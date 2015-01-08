# Microsoft SQL Server puppet module.

This module installs Microsoft SQL Server 2008 R2 on Windows 2012 R2.

## Installation

This module depends on DISM module to enable .net 3.5 on Windows Server:

* [dism module](http://forge.puppetlabs.com/puppetlabs/dism)

## Configuration

The installer supports the following options:

    media          = 'D:\\',
    instancename   = 'MSSQLSERVER',
    features       = 'SQL,AS,RS,IS',
    agtsvcaccount  = 'SQLAGTSVC',
    agtsvcpassword = 'Sql!@gt#2008demo',
    assvcaccount   = 'SQLASSVC',
    assvcpassword  = 'Sql!@s#2008demo',
    rssvcaccount   = 'SQLRSSVC',
    rssvcpassword  = 'Sql!Rs#2008demo',
    sqlsvcaccount  = 'SQLSVC',
    sqlsvcpassword = 'Sql!#2008demo',
    instancedir    = "C:\\Program Files\\Microsoft SQL Server",
    ascollation    = 'Latin1_General_CI_AS',
    sqlcollation   = 'SQL_Latin1_General_CP1_CI_AS',
    admin          = 'Administrator'
	securitymode   = 'SQL'
	sapassword	   = 'Sa!#2008demo'

### Example
	class { 'mssql': 
		media => 'D:\\',
		instancename => 'MSSQLSERVER',
		features => 'SQL,AS,RS,IS',
		agtsvcaccount  => 'SQLAGTSVC',
		agtsvcpassword => 'Sql!@gt#2008demo',
		assvcaccount   => 'SQLASSVC',
		assvcpassword  => 'Sql!@s#2008demo',
		rssvcaccount   => 'SQLRSSVC',
		rssvcpassword  => 'Sql!Rs#2008demo',
		sqlsvcaccount  => 'SQLSVC',
		sqlsvcpassword => 'Sql!#2008demo',
		instancedir    => "C:\\Program Files\\Microsoft SQL Server",
		ascollation    => 'Latin1_General_CI_AS',
		sqlcollation   => 'SQL_Latin1_General_CP1_CI_AS',
		admin          => 'Administrator'
		securitymode   => 'SQL'
		sapassword	   => 'Sa!#2008demo'
	}

### Notes
#### instancedir
The path should be specified without a trailing backslash. The following formats are supported [[ref]](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/af3bb5ed-0f4b-4c8a-8b12-826bccb850b8/sql-08-r2-standard-x64-installation-failure-illegal-characters-in-path?forum=sqlsetupandupgrade "ref"):
	
- `/INSTANCEDIR=c:\PathName` is supported.
- `/INSTANCEDIR=c:\PathName\` is supported.
- `/INSTANCEDIR="c:\PathName\\"` is supported.
- `/INSTANCEDIR="c:\PathName\"` is not supported.

The module will place the parameter's value into the config.ini where it will be contained in quotes.
 
#### agtsvcpassword | assvcpassword | rssvcpassword | sqlsvcpassword
The password must conform to the Windows Server password policy, namely:

- Passwords must not contain the entire account name or display name
- Passwords must contain 3 of
	- Uppercase character
	- Lowercase character
	- Base 10 digit
	- Nonalphanumeric character
	- Any alphabetic Unicode character not categorised as uppercase or lowercase 

[more detail...](http://technet.microsoft.com/en-gb/library/cc786468(v=ws.10).aspx)

#### securitymode
This may be SQL for Mixed Mode Authentication, or left blank/empty for Windows Authentication.

### More Options
See http://msdn.microsoft.com/en-us/library/ms144259.aspx for more information about these options.
