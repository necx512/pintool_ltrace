# pintool_ltrace

From https://gist.githubusercontent.com/PollyP/e50959ab97b15c83d4506dcf38753ef5/raw/4a0d7815991b47f61e832d45896b354d6c305a62/intel_pintools_vs2019.md

### Building Intel pintools with Visual Studio 2019 on Windows 10

#### Setting up the Intel pin build environment

I started with a Windows 10 Enterprise Evaluation VM, version 1809, from here: 
https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/ Then I installed the needed tools:

- Install Visual Studio Community 2019 Edition from https://visualstudio.microsoft.com/downloads/, version 16.4.2. 
Make sure to install the Desktop development for C++ workload.

- Install GNU's make, version 4.2.1, using Cygwin's 64-bit installer. Cygwin installer link here: https://cygwin.com/install.html.

- If needed, create VS 32- and 64-bit developer command windows shortcuts. 

    My 32-bit shortcut: %comspec% /k ""C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\Build\vcvars32.bat""
    
    My 64-bit shortcut: %comspec% /k ""C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\Build\vcvars64.bat"".

- Install the Windows version of Intel pin tools from https://software.intel.com/en-us/articles/pin-a-binary-instrumentation-tool-downloads. 
I used Intel pin version pin-3.11-97998-g7ecce2dac-msvc-windows. 

#### Building and running an example pintool to use with a 32-bit process

 - Open a VS 2019 32-bit developer command window
 - Cd to the source\tools\SimpleExamples folder in the Intel pin folder
 - Add the Cygwin bin directory to your path: 
    set PATH=%PATH%;\cygwin64\bin
 - Build the pintool DLL:
    make obj-ia32/icount.dll TARGET=ia32
 - Now run the pintool against your application. 
 In this case, I have the 32-bit version of pslist.exe from the System Internals Suite in my home directory:
 
    ..\\..\\..\\pin.exe -t obj-ia32\icount.dll -- c:\Users\IEUser\pslist.exe
    
The instruction count will print out at the end of the pslist.exe output.

#### Building and running an example pintool to use with a 64-bit process

 - Open a VS 2019 64-bit developer command window
 - Cd to the source\tools\SimpleExamples folder in the Intel pin folder
 - Add the Cygwin bin directory to your path: 
    set PATH=%PATH%;\cygwin64\bin
 - Build the pintool DLL:
    make obj-intel64/icount.dll TARGET=intel64
 - Now run the pintool against your application. 
 In this case, I have the 64-bit version of pslist.exe from the System Internals Suite in my home directory:
 
    ..\\..\\..\pin.exe -t obj-intel64\icount.dll -- c:\Users\IEUser\pslist64.exe
    
The instruction count will print out at the end of the pslist64.exe output.


# Note:
cl.exe est en 32 bits si je le lance avec vs code.
Dans la barre de recherche windows, j'ai donc chercher "x64 Native Tools Command Prompt"
