# ISSC
Скрипт получения информации о состоянии компьютера

Используется 2 модуля и 1 скрипт запуска 5 конфигурационных файлов:

- [PSWriteExcel] - [разработка позаимствована из репозитория EvotecIT](https://github.com/EvotecIT/PSWriteExcel)
- [ISSC_modules] - Собственная разработка с использованием функций найденных на просторах Интернет

- [AssetInspections.ps1] - Скрипт запуска проверок

- [Main.Ini] - Файл конфигурации редко меняющихся переменных
- [Param_XXX.ini] - Файл конфигурации функций проверки состояния ПК
- [ListDir] - Это параметр из конфигурационного файла Param_xxx.ini. Содержит путь до текстового файла со списком директорий, которые необходимо проверить на доступность и вывести их содержимое.
- [ListFile] - Это параметр из конфигурационного файла Param_xxx.ini. Содержит путь до текстового файла со списком файлов, которые необходимо проверить на доступность.
- [ListKey] - Список веток реестра и параметров с ключами для проверки их присутствия на тестируемом ПК.

# ToDo

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
- [ ] Список пользователей в указанной в списке группе
- [x] Список файлов в каталогах по списку
- [x] Список наличия или отсутствия файлов по списку
- [x] Список значения ключей реестра по списку
- [ ] Список значений параметров ГПО по списку

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
- [ ] Get-LocalGroupMembers - Функция вывода локальных пользователей и групп. Разработана, но фактически не используется
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

### Конфигурационный файл
Передача переменных осуществляется из *.INI файлов, разделенных на два файла Main.Ini и Param_XXXX.ini
#### Main.Ini находятся редко меняемые переменные:
```cmd
[AsExcel]
Enabled=true
Path=C:\sys\KIRB_Remote\sys\script\DeveloperScript\dev\ISSC\Data\XLSX\
DateFormat=yyyyMMdd-HH
;Тут может быть комментарий
[AsJSON]
Enabled=true
Compress=false
Path=C:\sys\KIRB_Remote\sys\script\DeveloperScript\dev\ISSC\Data\JSON\
DateFormat=yyyyMMdd-HH
;Тут может быть комментарий
[Logging]
ConsoleEnable=true
ShowTime=true
LogDir=C:\sys\KIRB_Remote\sys\script\DeveloperScript\dev\ISSC\Log\
LogFile=Loging.log
ErrLogdir=C:\sys\KIRB_Remote\sys\script\DeveloperScript\dev\ISSC\Log\
ErrLogFile=Error.log
LogTimeFormat=HH:mm:ss yyyy/MM/dd
```

#### Param_XXX.ini находяться оперативно изменяемые переменные:
```cmd
[StandaloneWrk]
Enabled=true
ArrWrk=jmike
;Тут может быть комментарий
[DomainWrk]
Enabled=false
CheckUO="OU=Osliq,OU=LTSC,OU=Users,OU=WorkStation,DC=ueb,DC=local"
DCName="MT-DC01.ueb.local"
;Тут может быть комментарий
[CheckModule]
ALL=false
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
;Тут может быть комментарий
[CheckList]
Enable=True
ListDir="C:\sys\KIRB_Remote\sys\script\DeveloperScript\dev\ISSC\CFG\ListDir1.txt"
ListFile="C:\sys\KIRB_Remote\sys\script\DeveloperScript\dev\ISSC\CFG\ListFile1.txt"
ListKey="C:\sys\KIRB_Remote\sys\script\DeveloperScript\dev\ISSC\CFG\ListKey1.txt"
```
##### Раздел [CheckList]
В данном разделе указываются списки проверок Директорий, Файлов, Ключей реестра на доступность.

- ListDir Список директорий, которые необходимо проверить на доступность. Просмотреть содерживое этих директорий
- ListFile Список файлов, которые необходимо проверить на доступность
- ListKey Список веток реестра и параметров с ключами для проверки их присутствия на тестируемом ПК

#### Запускающий скрипт 

```powershell
<#	
	.NOTES
	===========================================================================
	 Created with: 	SAPIEN Technologies, Inc., PowerShell Studio 2020 v5.7.172
	 Created on:   	29.04.2020 10:08
	 Created by:   	Nekhoroshev Michael
	 Organization: 	Nornik
	 Filename:     	Test-Module.ps1
	===========================================================================
	.DESCRIPTION
	Скрипт для запука  
#>
#requires -Version 5
#requires -RunAsAdministrator

Import-Module -Name "C:\sys\KIRB_Remote\sys\script\DeveloperScript\dev\ISSC\Module\PSWriteExcel"

Import-Module -Name "C:\sys\KIRB_Remote\sys\script\DeveloperScript\dev\ISSC\Module\ISSC"


#Run each module function
Clear-Host
start-Inventory -MainFilePath ".\main.ini" -ParamFilePath ".\CFG\Param.ini" -Periodic $true
# Параметр -Periodic определяет периодичность проверки.
# Если True - скрипт предназначен для регулярного использования по расписанию
# Если False - скрипт предназначен для периодического использования. В этом случае после удачной проверки, конфигурационный файл Param_XXX.ini переименовывается в Param_XXX_DateTime.old и при следующие записи расписания скрипт игнорируется, задание завершается успешно.
```
