# PLC Programming using TwinCAT 3
## 1. Twincat 3 Introduction
Twincat 3 is developed by beckhoff infosys, most of the development practices in TC3 are for the field of automation, in general, it does not have its roots in the field of software engineering but, rather in electrical engineering. It has been used in manufacturing machines, machines converting wave energy into electricity, large optical telescopes(ESO-ELT).
![TwinCAT3](https://user-images.githubusercontent.com/59905905/215697233-753ac135-5855-4ea1-b04f-bc1b45fc76de.png)
## 2. History of TC3
Before plcs it was possible to automate process using relay based control systems. This approach however required huge amoun of relays, cables and alot of space, which were hard to maintain. In 1960s, the first idea for plcs came when companies like general motors and allen-bradley, introduced first plc system, the first plc was a modicon model 084.
## 3. Basics and Installation
The basic difference between the runtime and the development environment.
![image](https://user-images.githubusercontent.com/59905905/215706801-acc89c9b-5e58-4243-b0b1-80166b6e2ccf.png)
XAE - it stands for Extended automation engineering, this the development environment for TC3, it is integrated wih Visual Studio, it only runs on Windows
XAR - it stands for Extended automation runtime, XAR can be installed on windows and beckhoff's own operating system.
XAE and XAR communicate with each other using a protocol called ADS, TC3 can also interact with various sensors and actuators such as relays, valves and electric motors.
On installing the XAE, XAR is downloaded automatically, it allows us to run the twincat software locally on our development machine.
## 4. Print "Hello World"
1. Before staring with TwinCAT3 we need to do some changes in BIOS Settings of our development environment, we need to go into our BIOS Settings and enable Virtualization Extensions. 
2. Once the virtualization settings are enabled, start the twinCAT program and create a new project by clicking 'New Project' option available on the start page.
3. Now go to 'PLC' folder in Solution Explorer, and create a standard PLC Project named 'HelloWorldProject'. A new folder named 'HelloWorldProject' will be created under PLC folder.
4. Now go to realtime, it will open a dialog box, before moving on, make sure the runtime environment is set to Local, the dialog box shows the performance of the various cores of the system.
5. Now got to POUs, under POUs main program is present which will be used to write our Hello World programme.
6. To print Hello World we will use ADSLOGSTR to log the string Hello World using the ADS interface, the code will be: 
```
ADSLOGSTR(msgCtrlMask := ADSLOG_MSGTYPE_ERROR OR ADS_MSGTYPE_LOG,
          msgFmtStr := 'Hello %s',
          strArg := 'world!');
```
![image](https://user-images.githubusercontent.com/59905905/215728537-fb88f045-08ff-49ec-827c-035cbcdb3c60.png)
7. Write the following program in the MAIN file, in the IDE.
```
PROGRAM MAIN
VAR
  bRunOnlyOnce : BOOL := FAlSE;
END_VAR
```
```
IF NOT bRunOnlyOnce THEN
  ADSLOGSTR(msgCtrlMask := ADSLOG_MSGTYPE_ERROR OR ADS_MSGTYPE_LOG,
          msgFmtStr := 'Hello %s',
          strArg := 'world!');
  bRunOnlyOnce := TRUE;
END_IF
```
![image](https://user-images.githubusercontent.com/59905905/215728969-6f03c5b3-ccbf-41a3-bca7-2658f23e6332.png)

## 5. Data Types under IEC 61131-3 standards
TwinCAT is a static programming language in which the data type needs to declared for each Variable being used. In twinCAT 3 all variables are declared in tags "VAR" and "END_VAR".
```
VAR
  fCabinTemperature: REAL;
END_VAR
```
In the above example, only one variable id declared called 'fCAbinTemperature' and it is declared as a 'REAL' which is a floating point value.
### 5.1 Boolean
It is a data type containing two values , i.e. 'True' and 'False'
```
booleanVariable : BOOL := TRUE; 
```
Type  | Values | Memory Consumption
------------- | ------------- | ------------
Boolean  | TRUE(1)  | 8 Bits 
Boolean | FALSE(0)  | (1 Byte)
         
### 5.2 Integer  
Type  | Lower Bound | Upper Bound | Memory Consumption | Example
------|-------------|-------------|--------------------|---------
INT   | -32768      | 32768       | 16 bits(2 bytes)   | `nThisNumber : INT := -4232 `
UINT   | 0      | 65535       | 16 bits(2 bytes)   | `nThisNumber : UINT := 42320 `
SINT   | -128      | 127       | 8 bits(1 bytes)   | `nThisNumber : SINT := -32 `
USINT   | 0      | 255       | 8 bits(1 bytes)   | `nThisNumber : USINT := 32 `
DINT   | -2147483647      | 2147483647       | 32 bits(4 bytes)   | `nThisNumber : DINT := 136292311 `
UDINT   | 0      | 4294967295       | 32 bits(4 bytes)   | `nThisNumber : UDINT := 13629231231 `
LINT   | -2<sup>63</sup>      | 2<sup>63</sup> - 1       | 64 bits(8 bytes)   | `nThisNumber : LINT := 13629231231 `
ULINT   | 0      | 2<sup>64</sup> - 1       | 64 bits(8 bytes)   | `nThisNumber : ULINT := 13629231231 `
BYTE   | 0      | 255       | 8 bits(1 bytes)   | `nThisNumber : BYTE := 2#1101_0111 `
WORD   | 0      | 65535       | 16 bits(2 bytes)   | `nThisNumber : WORD := 16#02AE `
DWORD   | 0      | 4294967295       | 32 bits(4 bytes)   | `nThisNumber : DWORD := 16#02AE_FFFF `
LWORD   | 0      | 2<sup>64</sup> - 1       | 64 bits(8 bytes)   | `nThisNumber : LWORD := 10#2348820191829 `
REAL | -3.4 x 10<sup>38</sup> | 3.4 x 10<sup>38</sup> | 32 Bits(4 Bytes) | `nThisReal: REAL := 3.1417304632 `

### 5.3 String 
A variable of data type STRING can accept any string. The size specification for the memory space allocation in the declaration refers to characters and is enclosed by round or square brackets. If no size is specified, TwinCAT assumes 80 characters by default.
```
sVar : STRING(35) := 'This is a String';
```








