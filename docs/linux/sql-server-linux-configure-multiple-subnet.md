---
title: Настройка несколькими подсетями группы доступности AlwaysOn и экземпляров отказоустойчивых кластеров в Linux | Документация Майкрософт
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/01/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 4c8116462266386457270b16ebcdb684252f5dcf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713256"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>Настройка несколькими подсетями группы доступности AlwaysOn и экземпляров отказоустойчивых кластеров

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Когда всегда в группе доступности (AG) или отработки отказа экземпляра кластера (FCI) охватывает более одного узла, каждый узел обычно имеет свой собственный сети. Часто это означает, что каждый узел имеет свой собственный IP-адреса. Например адреса сайтов A начать с 192.168.1. *x* и адреса сайта Б будет начинаться с 192.168.2. *x*, где *x* является частью IP-адрес, который является уникальным на сервере. Без какого то маршрутизации на сетевом уровне эти серверы не будут могут связываться друг с другом. Существует два способа для обработки этого сценария: Настройка сети, которая соединяет два разных подсетях, известный как виртуальной локальной сети, или настройте маршрутизацию между подсетями.

## <a name="vlan-based-solution"></a>Решение на основе виртуальной ЛС
 
**Готовности к установке**: Для решения на основе виртуальной ЛС на каждом сервере, участвующих в группе Доступности или экземпляра отказоустойчивого Кластера должно двумя сетевыми картами (NIC) для правильной доступности (двухпортовый сетевой Адаптер будет единой точки отказа на физическом сервере), чтобы его можно назначить IP-адресов на его собственном подсети, а также один в виртуальной локальной сети. Это дополнение к любых других сведений сети, например iSCSI, которое также требует собственной сети.

Создание адреса IP-адрес для группы Доступности или экземпляра отказоустойчивого Кластера выполняется на виртуальной локальной сети. В следующем примере локальная сеть имеет подсети 192.168.3. *x*, поэтому 192.168.3.104 IP-адрес, созданный для группы Доступности или экземпляра отказоустойчивого Кластера. Никакой дополнительной необходимо настроить, так как один IP-адрес, назначенный группе Доступности или экземпляра отказоустойчивого Кластера.

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Конфигурации с помощью Pacemaker

В мире Windows отказоустойчивого кластера Windows Server (WSFC) изначально поддерживает несколько подсетей и обрабатывает несколько IP-адресов через зависимость или IP-адреса. В Linux нет никакой зависимости OR, но есть способ добиться правильного несколькими подсетями в собственном коде с помощью Pacemaker, как показано ниже. Это невозможно, просто используя обычной командной строки Pacemaker изменение ресурса. Вам потребуется изменить сведения о кластере базовый (CIB). CIB является XML-файл с конфигурацией Pacemaker.

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>Обновление CIB

1.  Экспортируйте CIB.

    **Red Hat Enterprise Linux (RHEL) и Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    Где *filename* — это имя, необходимо вызвать CIB.

2.  Измените файл, который был создан. Найдите `<resources>` раздел. Вы увидите различные ресурсы, которые были созданы для группы Доступности или экземпляра отказоустойчивого Кластера. Найти связанную с IP-адрес. Добавить `<instance attributes>` разделе данными для второй IP-адрес выше или ниже существующей, но перед `<operations>`. Это похоже на следующий синтаксис:

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    где *NameForAttribute* — уникальное имя для этого атрибута *Оценка* — это номер, присвоенный атрибут, который должен быть выше, чем первичная подсеть, *RuleName*— имя правила, *имя* имя выражения, *NodeNameInSubnet2* — это имя узла в другой подсети, *NameForSecondIP* — это имя, связанное с IP-адрес второй *IPAddress* IP-адрес для второй подсети *NameForSecondIPNetmask* — это имя, связанное с маску подсети, и *Маску подсети* — это маска для второй подсети.
    
    Ниже показан пример.
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  Импортируйте измененный CIB и перенастроить Pacemaker.

    **RHEL или Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    где *filename* имя файла CIB с измененный IP-адресе.

### <a name="check-and-verify-failover"></a>Проверьте и проверьте отработку отказа

1.  После успешного применения CIB обновленной конфигурации проверьте связь с DNS-имя, связанное с ресурс IP-адреса в Pacemaker. Оно должно отражать IP-адрес, связанный с подсетью, в настоящее время размещается группа Доступности или экземпляра отказоустойчивого Кластера.
2.  Сбой группы Доступности или экземпляра отказоустойчивого Кластера к другой подсети.
3.  После того как группы Доступности или экземпляра отказоустойчивого Кластера полностью online, проверьте связь с DNS-имя, связанное с IP-адрес. Оно должно отражать IP-адрес в подсети второй.
4.  При необходимости, происходит переключение группы Доступности или экземпляра отказоустойчивого Кластера исходная.
