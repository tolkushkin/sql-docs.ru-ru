---
title: UTF8 Строковый определяемый пользователем тип (UDT) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: 41b84606-1fa8-4e4b-8f4c-bdc66537c613
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 824a722c527b600fd09c8f68725ad033ab1a1b8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62780171"
---
# <a name="utf8-string-user-defined-data-type-udt"></a>UTF8 String User-Defined Data Type (UDT)
  Образец UTF8String для SQL Server демонстрирует реализацию определяемого пользователем типа данных. Этот образец показывает реализацию определяемого пользователем типа данных UTF8, который расширяет систему типов базы данных, обеспечивая возможность хранения значений в кодировке UTF8. Этот тип также реализует программный код для преобразования строк в Юникоде в формат UTF8 и обратно.  
  
## <a name="prerequisites"></a>предварительные требования  
 Для создания и запуска этого проекта должно быть установлено следующее программное обеспечение:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express можно получить бесплатно на [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] веб-сайте [с документацией и примерами по](https://go.microsoft.com/fwlink/?LinkId=31046)Express.  
  
-   База данных AdventureWorks, доступная на [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] веб-сайте [разработки](https://go.microsoft.com/fwlink/?linkid=62796).  
  
-   Пакет SDK 2.0 для платформы .NET Framework или более поздняя версия либо среда Microsoft Visual Studio 2005 или более поздняя версия. Пакет SDK для платформы .NET Framework можно получить бесплатно.  
  
-   Кроме того, должны выполняться следующие условия.  
  
-   Для используемого экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] должна быть включена интеграция со средой CLR.  
  
-   Чтобы включить интеграцию со средой CLR, выполните следующие действия.  
  
    #### <a name="enabling-clr-integration"></a>Включение интеграции со средой CLR  
  
    -   Выполните следующие команды [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  Чтобы включить CLR, необходимо иметь разрешение `ALTER SETTINGS` на уровне сервера, которое неявно предоставляется членам предопределенных ролей сервера `sysadmin` и `serveradmin`.  
  
-   На используемом экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] должна быть установлена база данных AdventureWorks.  
  
-   Если вы не являетесь администратором используемого экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , то для завершения установки необходимо, чтобы администратор предоставил вам разрешение **CreateAssembly**  .  
  
## <a name="building-the-sample"></a>Построение образца  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>Создайте и запустите образец в соответствии со следующими инструкциями.  
  
1.  Откройте командную строку Visual Studio или .NET Framework.  
  
2.  Если необходимо, создайте каталог для своего образца. В данном примере будет использоваться каталог C:\MySample.  
  
3.  В каталоге c:\MySample создайте файл `Utf8String.vb` (для образца на языке Visual Basic) или `Utf8String.cs` (для образца на языке C#) и скопируйте в него соответствующий образец кода на языке Visual Basic или C#, приведенный ниже.  
  
4.  Скомпилируйте образец кода из командной строки, выполнив одну из следующих команд, в зависимости от выбранного языка.  
  
5.  `Vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /target:library Utf8String.vb`  
  
6.  `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.XML.dll /target:library Utf8String.cs`  
  
7.  Скопируйте код установки [!INCLUDE[tsql](../../includes/tsql-md.md)] в файл и сохраните его в файле `Install.sql` в том же каталоге.  
  
8.  Если образец установлен в каталоге, отличном от `C:\MySample\`, внесите изменения в файл `Install.sql` , указав там этот каталог.  
  
9. Разверните сборку и хранимую процедуру, выполнив  
  
    -   `sqlcmd -E -I -i install.sql`  
  
10. Скопируйте скрипт проверки [!INCLUDE[tsql](../../includes/tsql-md.md)] в файл и сохраните его в файле `test.sql` в том же каталоге.  
  
11. Выполните скрипт проверки следующей командой  
  
    -   `sqlcmd -E -I -i test.sql`  
  
12. Скопируйте скрипт очистки [!INCLUDE[tsql](../../includes/tsql-md.md)] в файл и сохраните его в файле `cleanup.sql` в том же каталоге.  
  
13. Выполните скрипт следующей командой  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>Образец кода  
 Ниже приведены листинги кода для данного образца.  
  
 C#  
  
```  
using System;  
using System.Xml;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using System.Globalization;  
using Microsoft.SqlServer.Server;  
using System.Runtime.CompilerServices;  
using System.Reflection;  
  
    [Serializable]  
    [Microsoft.SqlServer.Server.SqlUserDefinedType(Microsoft.SqlServer.Server.Format.UserDefined, IsByteOrdered = true, MaxByteSize = 8000)]  
    public class Utf8String : INullable, IComparable, Microsoft.SqlServer.Server.IBinarySerialize  
    {  
        #region conversion to/from Unicode strings  
        /// <summary>  
        /// Parse the given string and return a utf8 representation for it.  
        /// </summary>  
        /// <param name="sqlString"></param>  
        /// <returns></returns>  
        public static Utf8String Parse(SqlString sqlString)  
        {  
            if (sqlString.IsNull)  
                return Utf8String.Null;  
  
            return new Utf8String(sqlString.Value);  
        }  
  
        /// <summary>  
        /// Get/Set the utf8 bytes for this string.  
        /// </summary>  
        public SqlBinary Utf8Bytes  
        {  
            get  
            {  
                if (this.IsNull)  
                    return SqlBinary.Null;  
  
                if (this.m_Bytes != null)  
                    return this.m_Bytes;  
  
                if (this.m_String != null)  
                {  
                    this.m_Bytes = System.Text.Encoding.UTF8.GetBytes(this.m_String);  
                    return new SqlBinary(this.m_Bytes);  
                }  
  
                throw new NotSupportedException("cannot return bytes for empty instance");  
            }  
            set  
            {  
                if (value.IsNull)  
                {  
                    this.m_Bytes = null;  
                    this.m_String = null;  
                }  
                else  
                {  
                    this.m_Bytes = value.Value;  
                    this.m_String = null;  
                }  
            }  
        }  
  
        /// <summary>  
        /// Return a unicode string for this type.  
        /// </summary>  
        [Microsoft.SqlServer.Server.SqlMethod(IsDeterministic = true, IsPrecise = true, DataAccess = Microsoft.SqlServer.Server.DataAccessKind.None, SystemDataAccess = Microsoft.SqlServer.Server.SystemDataAccessKind.None)]  
        public override string ToString()  
        {  
            if (this.IsNull)  
                return null;  
  
            if (this.m_String != null)  
                return this.m_String;  
  
            if (this.m_Bytes != null)  
            {  
                this.m_String = System.Text.Encoding.UTF8.GetString(this.m_Bytes);  
                return this.m_String;  
            }  
  
            throw new NotSupportedException("don't know how to return string from empty instance");  
        }  
  
        /// <summary>  
        /// Return a SqlStr  
        /// </summary>  
        public SqlString ToSqlString()  
        {  
            if (this.IsNull)  
                return SqlString.Null;  
  
            return new SqlString(this.ToString());  
        }  
  
        private SqlString GetSortKeyUsingCultureInternal(CultureInfo culture, bool ignoreCase,  
            bool ignoreNonSpace, bool ignoreWidth)  
        {  
            if (this.IsNull)  
                return SqlString.Null;  
  
            SqlCompareOptions compareOptions = SqlCompareOptions.None;  
            if (ignoreCase)   
                compareOptions = compareOptions | SqlCompareOptions.IgnoreCase;  
  
            if (ignoreNonSpace)   
                compareOptions = compareOptions | SqlCompareOptions.IgnoreNonSpace;  
  
            if (ignoreWidth)   
                compareOptions = compareOptions | SqlCompareOptions.IgnoreWidth;  
  
            return new SqlString(this.ToString(), culture.LCID, compareOptions);  
        }  
  
        [Microsoft.SqlServer.Server.SqlMethod(IsDeterministic = true, IsPrecise = true)]  
        public SqlString GetSortKeyUsingCulture(string cultureName, bool ignoreCase,  
            bool ignoreNonSpace, bool ignoreWidth)  
        {  
            CultureInfo culture = CultureInfo.CreateSpecificCulture(cultureName);  
            if (culture == null)  
                throw new ArgumentException(string.Format(  
                    CultureInfo.InvariantCulture,  
                    "Culture {0} not recognized.", cultureName));  
  
            return this.GetSortKeyUsingCultureInternal(culture, ignoreCase,   
                ignoreNonSpace, ignoreWidth);  
        }  
  
        [Microsoft.SqlServer.Server.SqlMethod(IsDeterministic = false)]  
        public SqlString GetSortKey(bool ignoreCase, bool ignoreNonSpace, bool ignoreWidth)  
        {  
            return this.GetSortKeyUsingCultureInternal(CultureInfo.CurrentCulture,  
                ignoreCase, ignoreNonSpace, ignoreWidth);  
        }  
  
        #endregion  
  
        #region comparison operators  
        public override bool Equals(object obj)  
        {  
            return this.CompareTo(obj) == 0;  
        }  
  
        public static bool operator ==(Utf8String utf8String, Utf8String other)  
        {  
            if (utf8String.IsNull) throw new ArgumentException(string.Empty);  
            return utf8String.Equals(other);  
        }  
  
        public static bool operator !=(Utf8String utf8String, Utf8String other)  
        {  
            return !(utf8String == other);  
        }  
  
        public static bool operator <(Utf8String utf8String, Utf8String other)  
        {  
            if (utf8String == null) throw new ArgumentException(string.Empty);  
            return (utf8String.CompareTo(other) < 0);  
        }  
  
        public static bool operator >(Utf8String utf8String, Utf8String other)  
        {  
            if (utf8String == null) throw new ArgumentException(string.Empty);  
            return (utf8String.CompareTo(other) > 0);  
        }    
  
        private int CompareUsingCultureInternal(Utf8String other, CultureInfo culture, bool ignoreCase,  
            bool ignoreNonSpace, bool ignoreWidth)  
        {  
            // By definition  
            if (other == null)   
                return 1;  
  
            if (this.IsNull)  
                if (other.IsNull)  
                    return 0;  
                else  
                    return -1;  
  
            if (other.IsNull)   
                return 1;  
  
            return this.GetSortKeyUsingCultureInternal(culture, ignoreCase, ignoreNonSpace,  
                ignoreWidth).CompareTo(other.GetSortKeyUsingCultureInternal(culture, ignoreCase,  
                ignoreNonSpace, ignoreWidth));  
        }  
  
        public int CompareUsingCulture(Utf8String other, string cultureName, bool ignoreCase,  
            bool ignoreNonSpace, bool ignoreWidth)  
        {  
            CultureInfo culture = CultureInfo.CreateSpecificCulture(cultureName);  
            if (culture == null)  
                throw new ArgumentException(string.Format(  
                    CultureInfo.InvariantCulture,   
                    "Culture {0} not recognized.", cultureName));  
  
            return this.CompareUsingCultureInternal(other, culture, ignoreCase,  
                ignoreNonSpace, ignoreWidth);  
        }  
  
        public int Compare(Utf8String other, bool ignoreCase,  
            bool ignoreNonSpace, bool ignoreWidth)  
        {  
            return this.CompareUsingCultureInternal(other, CultureInfo.CurrentCulture, ignoreCase,  
                ignoreNonSpace, ignoreWidth);  
        }  
  
        public override int GetHashCode()  
        {  
            if (this.IsNull)  
                return 0;  
  
            return this.ToString().GetHashCode();  
        }  
  
        public int CompareTo(object obj)  
        {  
            if (obj == null)  
                return 1; //by definition  
  
            Utf8String s = obj as Utf8String;  
  
            if (s == null)  
                throw new ArgumentException("the argument to compare is not a Utf8String");  
  
            if (this.IsNull)  
            {  
                if (s.IsNull)  
                    return 0;  
  
                return -1;  
            }  
  
            if (s.IsNull)  
                return 1;  
  
            return this.ToString().CompareTo(s.ToString());  
        }  
  
        #endregion  
  
        #region private state and constructors  
        private string m_String;  
  
        private byte[] m_Bytes;  
  
        public Utf8String(string value)  
        {  
            this.m_String = value;  
        }  
  
        public Utf8String(byte[] bytes)  
        {  
            this.m_Bytes = bytes;  
        }  
        #endregion  
  
        #region UserDefinedType boilerplate code  
  
        public bool IsNull  
        {  
            get  
            {  
                return this.m_String == null && this.m_Bytes == null;  
            }  
        }  
  
        public static Utf8String Null  
        {  
            get  
            {  
                Utf8String str = new Utf8String((string)null);  
  
                return str;  
            }  
        }  
  
        public Utf8String()  
        {  
        }  
        #endregion  
  
        #region IBinarySerialize Members  
        public void Write(System.IO.BinaryWriter w)  
        {  
            if (w == null) throw new ArgumentException(string.Empty);  
            byte header = (byte)(this.IsNull ? 1 : 0);  
  
            w.Write(header);  
            if (header == 1)  
                return;  
  
            byte[] bytes = this.Utf8Bytes.Value;  
  
            w.Write(bytes.Length);  
            w.Write(bytes);  
        }  
  
        public void Read(System.IO.BinaryReader r)  
        {  
            if (r == null) throw new ArgumentException(string.Empty);  
            byte header = r.ReadByte();  
  
            if ((header & 1) > 0)  
            {  
                this.m_Bytes = null;  
                return;  
            }  
  
            int length = r.ReadInt32();  
  
            this.m_Bytes = r.ReadBytes(length);  
        }  
        #endregion  
    }  
  
```  
  
 Visual Basic  
  
```  
Imports Microsoft.SqlServer.Server  
Imports Microsoft.VisualBasic  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlTypes  
Imports System.Diagnostics  
Imports System.Globalization  
<Serializable(), Microsoft.SqlServer.Server.SqlUserDefinedType(Microsoft.SqlServer.Server.Format.UserDefined, IsByteOrdered:=True, MaxByteSize:=8000), CLSCompliant(False)> _  
Public Class Utf8String  
    Implements INullable, IComparable, Microsoft.SqlServer.Server.IBinarySerialize  
#Region "Conversion to/from Unicode strings"  
    ''' <summary>  
    ''' Parse the given string and return a utf8 representation for it.  
    ''' </summary>  
    ''' <param name="sqlString"></param>  
    ''' <returns></returns>  
    Public Shared Function Parse(ByVal sqlString As SqlString) As Utf8String  
        If sqlString.IsNull Then  
            Return Utf8String.Null  
        End If  
  
        Return New Utf8String(sqlString.Value)  
    End Function  
  
    ''' <summary>  
    ''' Get/Set the utf8 bytes for this string.  
    ''' </summary>  
    Public Property Utf8Bytes() As SqlBinary  
        Get  
            If Me.IsNull Then  
                Return SqlBinary.Null  
            End If  
  
            If Not (Me.privBytes Is Nothing) Then  
                Return Me.privBytes  
            End If  
  
            If Not (Me.privString Is Nothing) Then  
                Me.privBytes = System.Text.Encoding.UTF8.GetBytes(Me.privString)  
                Return New SqlBinary(Me.privBytes)  
            End If  
  
            Throw New NotSupportedException("Cannot return bytes for empty instance")  
        End Get  
        Set(ByVal value As SqlBinary)  
            If value.IsNull Then  
                Me.privBytes = Nothing  
                Me.privString = Nothing  
            Else  
                Me.privBytes = value.Value  
                Me.privString = Nothing  
            End If  
        End Set  
    End Property  
  
    ''' <summary>  
    ''' Return a unicode string for this type.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlMethod(IsDeterministic:=True, IsPrecise:=True, DataAccess:=Microsoft.SqlServer.Server.DataAccessKind.None, SystemDataAccess:=Microsoft.SqlServer.Server.SystemDataAccessKind.None)> _  
    Public Overrides Function ToString() As String  
        If Me.IsNull Then  
            Return Nothing  
        End If  
  
        If Not (Me.privString Is Nothing) Then  
            Return Me.privString  
        End If  
  
        If Not (Me.privBytes Is Nothing) Then  
            Me.privString = System.Text.Encoding.UTF8.GetString(Me.privBytes)  
            Return Me.privString  
        End If  
  
        Throw New NotSupportedException("dont know how to return string from empty instance")  
    End Function  
  
    ''' <summary>  
    ''' Return a SqlStr  
    ''' </summary>  
    Public Function ToSqlString() As SqlString  
        If Me.IsNull Then  
            Return SqlString.Null  
        End If  
  
        Return New SqlString(Me.ToString())  
    End Function  
  
    Private Function GetSortKeyUsingCultureInternal(ByVal culture As CultureInfo, ByVal ignoreCase As Boolean, _  
    ByVal ignoreNonSpace As Boolean, ByVal ignoreWidth As Boolean) As SqlString  
        If Me.IsNull Then  
            Return SqlString.Null  
        End If  
        Dim compareOptions As SqlCompareOptions = SqlCompareOptions.None  
        If ignoreCase Then  
            compareOptions = compareOptions Or SqlCompareOptions.IgnoreCase  
        End If  
        If ignoreNonSpace Then  
            compareOptions = compareOptions Or SqlCompareOptions.IgnoreNonSpace  
        End If  
        If ignoreWidth Then  
            compareOptions = compareOptions Or SqlCompareOptions.IgnoreWidth  
        End If  
        Return New SqlString(Me.ToString(), culture.LCID, compareOptions)  
    End Function  
  
    <Microsoft.SqlServer.Server.SqlMethod(IsDeterministic:=True, IsPrecise:=True)> _  
    Public Function GetSortKeyUsingCulture(ByVal cultureName As String, ByVal ignoreCase As Boolean, _  
    ByVal ignoreNonSpace As Boolean, ByVal ignoreWidth As Boolean) As SqlString  
        Dim culture As CultureInfo = CultureInfo.CreateSpecificCulture(cultureName)  
        If culture Is Nothing Then  
            Throw New ArgumentException(String.Format(CultureInfo.InvariantCulture, _  
            "Culture {0} not recognized.", cultureName))  
        End If  
  
        Return Me.GetSortKeyUsingCultureInternal(culture, ignoreCase, ignoreNonSpace, ignoreWidth)  
    End Function  
  
    <Microsoft.SqlServer.Server.SqlMethod(IsDeterministic:=True, IsPrecise:=True)> _  
    Public Function GetSortKey(ByVal ignoreCase As Boolean, ByVal ignoreNonSpace As Boolean, _  
    ByVal ignoreWidth As Boolean) As SqlString  
        Return Me.GetSortKeyUsingCultureInternal(CultureInfo.CurrentCulture, ignoreCase, ignoreNonSpace, ignoreWidth)  
    End Function  
  
#End Region  
  
#Region "Comparison operators"  
    Public Overrides Function Equals(ByVal obj As Object) As Boolean  
        Return Me.CompareTo(obj) = 0  
    End Function  
  
    Public Shared Operator =(ByVal utf8StringValue As Utf8String, ByVal other As Utf8String) As Boolean  
        If utf8StringValue Is Nothing Then  
            Throw New ArgumentException(String.Empty)  
        End If  
        Return utf8StringValue.Equals(other)  
    End Operator  
  
    Public Shared Operator <>(ByVal utf8StringValue As Utf8String, ByVal other As Utf8String) As Boolean  
        Return Not (utf8StringValue = other)  
    End Operator  
  
    Public Shared Operator <(ByVal utf8StringValue As Utf8String, ByVal other As Utf8String) As Boolean  
        If utf8StringValue Is Nothing Then  
            Throw New ArgumentException(String.Empty)  
        End If  
        Return (utf8StringValue.CompareTo(other) < 0)  
    End Operator  
  
    Public Shared Operator >(ByVal utf8StringValue As Utf8String, ByVal other As Utf8String) As Boolean  
        If utf8StringValue Is Nothing Then  
            Throw New ArgumentException(String.Empty)  
        End If  
        Return (utf8StringValue.CompareTo(other) > 0)  
    End Operator  
  
    Private Function CompareUsingCultureInternal(ByVal other As Utf8String, ByVal culture As CultureInfo, _  
        ByVal ignoreCase As Boolean, ByVal ignoreNonSpace As Boolean, _  
        ByVal ignoreWidth As Boolean) As Integer  
        'By definition  
        If other Is Nothing Then  
            Return 1  
        End If  
  
        If Me.IsNull Then  
            If other.IsNull Then  
                Return 0  
            Else  
                Return -1  
            End If  
        End If  
  
        If other.IsNull Then  
            Return 1  
        End If  
  
        Return Me.GetSortKeyUsingCultureInternal(culture, ignoreCase, ignoreNonSpace, _  
        ignoreWidth).CompareTo(other.GetSortKeyUsingCultureInternal(culture, ignoreCase, _  
        ignoreNonSpace, ignoreWidth))  
    End Function  
  
    Public Function CompareUsingCulture(ByVal other As Utf8String, ByVal cultureName As String, _  
        ByVal ignoreCase As Boolean, ByVal ignoreNonSpace As Boolean, _  
        ByVal ignoreWidth As Boolean) As Integer  
        Dim culture As CultureInfo = CultureInfo.CreateSpecificCulture(cultureName)  
        If culture Is Nothing Then  
            Throw New ArgumentException(String.Format(CultureInfo.InvariantCulture, _  
            "Culture {0} not recognized.", cultureName))  
        End If  
  
        Return Me.CompareUsingCultureInternal(other, culture, ignoreCase, _  
        ignoreNonSpace, ignoreWidth)  
    End Function  
  
    Public Function Compare(ByVal other As Utf8String, ByVal ignoreCase As Boolean, ByVal ignoreNonSpace As Boolean, _  
        ByVal ignoreWidth As Boolean) As Integer  
        Return Me.CompareUsingCultureInternal(other, CultureInfo.CurrentCulture, ignoreCase, _  
        ignoreNonSpace, ignoreWidth)  
    End Function  
  
    Public Overrides Function GetHashCode() As Integer  
        If Me.IsNull Then  
            Return 0  
        End If  
  
        Return Me.ToString().GetHashCode()  
    End Function  
  
    Public Function CompareTo(ByVal obj As Object) As Integer Implements IComparable.CompareTo  
        If obj Is Nothing Then  
            Return 1 'by definition  
        End If  
  
        Dim s As Utf8String = CType(obj, Utf8String)  
  
        If s Is Nothing Then  
            Throw New ArgumentException("the argument to compare is not a Utf8String")  
        End If  
  
        If Me.IsNull Then  
            If s.IsNull Then  
                Return 0  
            End If  
            Return -1  
        End If  
  
        If s.IsNull Then  
            Return 1  
        End If  
  
        Return Me.ToString().CompareTo(s.ToString())  
    End Function  
#End Region  
  
#Region "Private state and constructors"  
    Private privString As String  
    Private privBytes() As Byte  
  
    Public Sub New(ByVal value As String)  
        Me.privString = value  
        'Me.privBytes = Nothing  
    End Sub  
  
    Public Sub New(ByVal bytes() As Byte)  
        Me.privBytes = bytes  
        'Me.privString = Nothing  
    End Sub  
#End Region  
  
#Region "UserDefinedType boilerplate code"  
    Public ReadOnly Property IsNull() As Boolean Implements INullable.IsNull  
        Get  
            Return Me.privString Is Nothing AndAlso Me.privBytes Is Nothing  
        End Get  
    End Property  
  
    Public Shared ReadOnly Property Null() As Utf8String  
        Get  
            Dim str As New Utf8String(CStr(Nothing))  
  
            Return str  
        End Get  
    End Property  
  
    Public Sub New()  
    End Sub  
#End Region  
  
#Region "IBinarySerialize Members"  
    Public Sub Write(ByVal w As System.IO.BinaryWriter) Implements Microsoft.SqlServer.Server.IBinarySerialize.Write  
        If w Is Nothing Then  
            Throw New ArgumentException(String.Empty)  
        End If  
        Dim header As Byte  
        If (Me.IsNull) Then  
            header = 1  
        Else  
            header = 0  
        End If  
  
        w.Write(header)  
  
        If header = 1 Then  
            Return  
        End If  
  
        Dim bytes As Byte() = Me.Utf8Bytes.Value  
  
        w.Write(bytes.Length)  
        w.Write(bytes)  
    End Sub  
  
    Public Sub Read(ByVal r As System.IO.BinaryReader) Implements Microsoft.SqlServer.Server.IBinarySerialize.Read  
        If r Is Nothing Then  
            Throw New ArgumentException(String.Empty)  
        End If  
        Dim header As Byte = r.ReadByte()  
  
        If (header And 1) > 0 Then  
            Me.privBytes = Nothing  
            Return  
        End If  
  
        Dim length As Integer = r.ReadInt32()  
  
        Me.privBytes = r.ReadBytes(length)  
    End Sub  
#End Region  
End Class  
```  
  
 Это скрипт установки [!INCLUDE[tsql](../../includes/tsql-md.md)] (`Install.sql`), который выполняет развертывание сборки и создает в базе данных определяемый пользователем тип.  
  
```  
USE AdventureWorks;  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE ([name] = N'ResumeFullName') AND ([type] = 'FN'))  
DROP FUNCTION [dbo].[ResumeFullName];  
GO  
  
IF EXISTS (SELECT * FROM sys.indexes WHERE NAME = N'IX_utf8test_ustr')  
DROP INDEX utf8test.IX_utf8test_ustr;  
GO  
  
IF EXISTS (SELECT * FROM sys.tables WHERE name = N'utf8test')   
DROP TABLE [dbo].[utf8test];  
GO  
  
IF EXISTS (SELECT * FROM sys.tables WHERE name = N'ResumeNames')   
DROP TABLE [dbo].[ResumeNames];  
GO  
  
IF EXISTS (SELECT * FROM sys.types WHERE name = N'Utf8String')   
DROP TYPE [Utf8String];  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE name = N'UTF8String')   
DROP ASSEMBLY UTF8String;  
GO  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of the this variable if you have installed   
-- the sample someplace other than the default location.  
set @SamplesPath= N'C:\MySample\'  
  
CREATE ASSEMBLY UTF8String   
FROM @SamplesPath +'UTF8String.dll';  
GO  
  
CREATE TYPE [Utf8String]   
EXTERNAL NAME [UTF8String].[Utf8String];  
GO  
```  
  
 Это файл `test.sql`, который проверяет образец, тестируя его тип.  
  
```  
USE AdventureWorks;  
GO  
  
-- simple usage of the type in variables and select statements  
-- convert to string, binary, do a substring on it, get the utf8bytes  
DECLARE @u Utf8String;  
SET @u = CONVERT(Utf8String, 'hello world');  
SELECT @u.ToString(),   
    CONVERT(varbinary(8000), @u),  
    SUBSTRING(@u.ToString(), 1, 5),  
    @u.Utf8Bytes;  
GO  
  
-- create a table with this type  
CREATE TABLE utf8test(u Utf8String);  
GO  
  
-- populate it with some random data  
SET NOCOUNT ON;  
BEGIN TRAN;  
DECLARE @index int, @str nvarchar(4000);  
SET @index = 0;  
WHILE @index < 1000  
BEGIN  
    SET @str = CONVERT(nvarchar(100), @index);  
    INSERT INTO utf8test VALUES(CONVERT(Utf8String, @str))  
    SET @index = @index + 1;  
END  
COMMIT TRAN;  
GO  
  
-- Find a particular UTF8 string  
  
DECLARE @i int;  
SELECT @i = COUNT(*) from utf8test   
WHERE u = CONVERT(Utf8String, '100');  
SELECT @i;  
go  
  
-- Find UTF8 strings with a particular substring  
DECLARE @i int;  
SELECT @i = COUNT(*) from utf8test   
WHERE SUBSTRING(u.ToString(), 1, 1) = '1';  
SELECT @i;  
GO  
  
-- Add a computed column over the ToString method  
ALTER TABLE utf8test ADD ustr AS u.ToString() PERSISTED;  
GO  
  
-- Create an index over the computed column  
CREATE INDEX IX_utf8test_ustr ON utf8test(ustr);  
GO  
  
-- Binary comparisons on Utf8Strings are not effective.  Even if we use the ToString method  
-- to convert it to a string, we may want to have more control over whether case, width, or  
-- attributes are relevant to the comparison.  This portion of the test creates a table of   
-- localized data pulled from the resumes stored in the AdventureWorks database,  
-- and then demonstrates comparsions and sorting based on the CompareUsingCulture   
-- and GetSortKeyUsingCulture methods defined on Utf8String.  
  
IF EXISTS (SELECT * FROM sys.objects WHERE ([name] = N'ResumeFullName') AND ([type] = 'FN'))  
DROP FUNCTION [dbo].[ResumeFullName];  
GO  
  
-- Returns the complete name of the applicant from her resume.    
-- We don't just use data(/RES:Resume[1]/RES:Name) because we need spaces  
-- between each part of the name.  
CREATE FUNCTION ResumeFullName (@Resume xml)  
RETURNS nvarchar(100)  
AS  
BEGIN  
    RETURN CONVERT(nvarchar(100), @Resume.query(N'declare namespace RES="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/Resume"; for $b in /RES:Resume[1]/RES:Name/* return data($b)'));  
END  
GO  
  
SELECT Cast(RTRIM(LTRIM(dbo.ResumeFullName(Resume))) as Utf8String) AS FullName   
INTO ResumeNames FROM HumanResources.JobCandidate;  
GO  
  
SELECT FullName.ToString() FROM ResumeNames;  
  
DECLARE @Shai Utf8String;  
SET @Shai = N'Shai  Bassli';  
SELECT FullName.ToString() FROM ResumeNames   
WHERE FullName.CompareUsingCulture(@Shai, 'en-us', 1, 0, 0) = 0;  
GO  
  
ALTER TABLE ResumeNames ADD SortKey AS FullName.GetSortKeyUsingCulture('en-us', 1, 0, 0) PERSISTED;  
GO  
  
CREATE INDEX IX_ResumeNames_SortKey ON ResumeNames(SortKey);  
GO  
  
SELECT FullName.ToString()   
FROM ResumeNames  
ORDER BY SortKey;  
```  
  
 В следующем образце [!INCLUDE[tsql](../../includes/tsql-md.md)] сборка и тип удаляются из базы данных.  
  
```  
USE AdventureWorks;  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE ([name] = N'ResumeFullName') AND ([type] = 'FN'))  
DROP FUNCTION [dbo].[ResumeFullName];  
GO  
  
IF EXISTS (SELECT * FROM sys.indexes WHERE NAME = N'IX_utf8test_ustr')  
DROP INDEX utf8test.IX_utf8test_ustr;  
GO  
  
IF EXISTS (SELECT * FROM sys.tables WHERE name = N'utf8test')   
DROP TABLE [dbo].[utf8test];  
GO  
  
IF EXISTS (SELECT * FROM sys.tables WHERE name = N'ResumeNames')   
DROP TABLE [dbo].[ResumeNames];  
GO  
  
IF EXISTS (SELECT * FROM sys.types WHERE name = N'Utf8String')   
DROP TYPE [Utf8String];  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE name = N'UTF8String')   
DROP ASSEMBLY UTF8String;  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [Сценарии использования и примеры интеграции со средой CLR](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
