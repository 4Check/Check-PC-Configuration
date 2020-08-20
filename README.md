# ISSC v.3
Скрипт получения информации о состоянии компьютера

Конфигурационных состоит из:

- [PSWriteExcel] - [разработка позаимствована из репозитория EvotecIT](https://github.com/EvotecIT/PSWriteExcel)
- [ISSC.AD.Lib] - [Модуль получение данных из Active Directory. Автор:OneIdentity.com](https://www.oneidentity.com/products/active-roles/)
- [ISSC.Main.Lib] - Модуль функций получение информации о состоянии компьютера на момент сканирования.
- [ISSC.PowerShell.Archive.Lib] - [Модуль создания архивных файлов](https://docs.microsoft.com/ru-ru/powershell/module/microsoft.powershell.archive/?view=powershell-5.1)
- [ISSC.Startup.Lib] - Модуль функции запуска сканирования состояния компьютеров

- [AssetInspections.ps1] - Скрипт запуска проверок

- [Main.Ini] - Файл конфигурации редко меняющихся переменных
- [Param_XXX.ini] - Файл конфигурации функций проверки состояния ПК
- [ListDir] - Это параметр из конфигурационного файла Param_xxx.ini. Содержит путь до текстового файла со списком директорий, которые необходимо проверить на доступность и вывести их содержимое.
- [ListFile] - Это параметр из конфигурационного файла Param_xxx.ini. Содержит путь до текстового файла со списком файлов, которые необходимо проверить на доступность.
- [ListKey] - Список веток реестра и параметров с ключами для проверки их присутствия на тестируемом ПК.

# В планах....

### HARD
- [x] CPU (тип и частота)
- [x] RAM (всего/свободно)
- [x] HDD Диск С (всего/свободно)
- [x] Сетевые интерфейсы (ip, mac, dhcp)
- [x] Статические маршруты
### OS,Soft
- [x] ОС (наименование, версия, билд)
- [x] Список установленных обновлений
- [x] Список установленного ПО
### ACL
- [x] Список расшаренных папок
- [x] Список УЗ в группе локальных администраторов
- [ ] Список локальных пользователей
- [ ] Список локальных групп
### Status
- [x] Список запущенных служб с их состоянием
- [x] Список запущенных процессов
- [x] Список открытых портов и их владельцев
- [x] Текущий пользователь (локальный вход) 
### Custom
- [x] Список антивирусов установленных на ПК
- [x] Получение информации после выполнения команды 'winsat formal -restart'
- [x] Список файлов в каталогах по списку
- [x] Список наличия или отсутствия файлов по списку
- [x] Список значения ключей реестра по списку
- [ ] Список значений параметров ГПО по списку
- [ ] Архивирование результатов после сканирования
- [ ] Список пользователей в указанной в списке группе

### Выгрузка результатов
- [x] Excel - выгрузка без предустановленного ПО MS Office
- [x] JSON - с компресией или без

### Функции
- [x] Start-TimeLog - Функция запуска таймера в начале запуска скрипта
- [x] Stop-TimeLog - Функция остановки таймера в конце скрипта
- [x] Write-log - Функция логирования действий скрипта с выводом разными цветами
- [x] Write-CMTrace - Функция логирования в формате SCCM Trace (One Trace) 
- [x] Get-Error - Получение ошибок при выполнении скрипта из переменной $Global:Error и логирование ее через функцию Write-CMTrace
- [x] Get-IniContent - Чтение параметров для скрипта из INI файлов. Получение Секций, Ключей, Значений
- [x] Get-DirFileName - Получение списка диреторий и файлов на удаленной ПК, список директорий и файлов формируется из текстового файла.
- [x] Get-RegValue - Получение списка параметра реестра по списку из текстового файла и его значение.
- [x] Get-UserVariable - Функция получения пользовательских переменных
- [x] Get-DomainWrk - Функция получения ПК в определенной OU
- [x] get-netstat - Функция получения вывода команды  NETSTAT.EXE
- [x] Get-NIC - Функция поиска локальных интерфейсов, вывода IP, MASK, DNS, DHCP
- [x] Get-FullDriveInfo - Функция получение информации о жестких дисках и USB дисках установленных в ПК
- [x] Get-MicrosoftUpdates - Функция вывода установленых обновлений
- [x] Get-LocalAdminMembers - Функция вывода пользователей в группе локальных администраторов
- [x] Get-shared - Функция вывода расшареных ресурсов
- [x] Get-ComputerApplications - Функция вывода устновленного программного обеспечения
- [x] get-iproute - Функция вывода постоянных маршрутов
- [x] get-loggedonuser - Функция вывода залогиненых пользователей с указанием их типов
- [x] Get-ComputerMissingDrivers - Функция вывода драйверов имеющих ошибки
- [x] Get-FirmwareEnvironmentVariableAPI - Функция получения типа BIOS\UAFI
- [x] Get-ComputerCPU - Функция вывода информации об установленных процессорах
- [x] Get-ComputerGPU - Функция вывода информации об установленной видео карте
- [x] ConvertTo-OperatingSystem - Функция конвертации короткого представления ОС в ее наименование
- [x] Get-ComputerOperatingSystem - Функция поредоставления данных об ОС
- [x] Get-ComputerSystem - Функция предоставления данных об системном блоке
- [x] Get-ComputerProcess - Функция вывода запущенных процессов
- [x] Get-ComputerService - Функция вывода состояния сервисов
- [x] Start-Inventory - Функция сбора всех параметров и предоставления объектов для выгрухки в форматы Excel и JSON


# Конфигурационный файл
Передача переменных осуществляется из *.INI файлов, разделенных на два файла Main.Ini и Param_XXXX.ini
## Main.Ini находятся редко меняемые переменные:
```cmd
[AsExcel]
Enabled=true
Path=.\ISSC\Data\XLSX\
DateFormat=yyyyMMdd-HH
;Тут может быть комментарий
[AsJSON]
Enabled=true
Compress=false
Path=.\ISSC\Data\JSON\
DateFormat=yyyyMMdd-HH
;Тут может быть комментарий
[Logging]
ConsoleEnable=true
ShowTime=true
LogDir=.\ISSC\Log\
LogFile=Loging.log
ErrLogdir=.\ISSC\Log\
ErrLogFile=Error.log
LogTimeFormat=HH:mm:ss yyyy/MM/dd
```

## Param_XXX.ini находяться оперативно изменяемые переменные:
```cmd
;Файл конфигурации параметров проверки
;
[StandaloneWrk]
Enabled=true
ArrWrk=wrk1,wrk2
;
[DomainWrk]
Enabled=true
CheckUO="OU=OU_Computers,OU=OU_Groups,DC=NetBios,DC=Domain"
DCName="my_dc.netbios.domain"
;
[CheckModule]
ALL=True
SystemInfo=false
DiskInfo=false
NetStat=false
NIC=false
Udates=false
LocalAdmin=false
SharedFolders=false
InstalledApp=false
PersistentRoutes=false
OSProcesses=false
OSServices=false
OSMissingDrivers=false
OSLoggingUser=false
Antivirus=True
SysPerform=True
;
[CheckList]
Enable=true
ListDir=".\CFG\ListDir1.txt"
ListFile=".\CFG\ListFile1.txt"
ListKey=".\CFG\ListKey1.txt"

```
### Раздел [CheckList]
В данном разделе указываются списки проверок Директорий, Файлов, Ключей реестра на доступность.

- ListDir Список директорий, которые необходимо проверить на доступность. Просмотреть содерживое этих директорий
- ListFile Список файлов, которые необходимо проверить на доступность
- ListKey Список веток реестра и параметров с ключами для проверки их присутствия на тестируемом ПК

# Запускающий скрипт 

```powershell
#requires -Version 5
#requires -RunAsAdministrator

If (-not((Get-Module -Name "PSWriteExcel") -and (Get-Module -Name "ISSC.Main.Lib") -and (Get-Module -Name "ISSC.AD.Lib")-and (Get-Module -Name "ISSC.PowerShell.Archive.Lib") -and (Get-Module -Name "ISSC.Startup.Lib"))){
           
           
            $pathModule =".\Asset\Module\"
            
            Import-Module -Name $pathModule"ISSC.Startup.Lib"
            Import-Module -Name $pathModule"PSWriteExcel"   
            Import-Module -Name $pathModule"ISSC.Main.Lib"  
            Import-Module -Name $pathModule"ISSC.AD.Lib\ActiveRoles.ManagementShell.dll" -DisableNameChecking 
            Import-Module -Name $pathModule"ISSC.PowerShell.Archive.Lib"
            
                      
}
#Run each module function
Clear-Host
start-Inventory -MainFilePath ".\Asset\main.ini" -ParamFilePath ".\Asset\CFG\Param.ini" -Periodic $true


# Параметр -Periodic определяет периодичность проверки.
# Если True - скрипт предназначен для регулярного использования по расписанию
# Если False - скрипт предназначен для периодического использования. В этом случае после удачной проверки, конфигурационный файл Param_XXX.ini переименовывается в Param_XXX_DateTime.old и при следующие записи расписания скрипт игнорируется, задание завершается успешно.
```
