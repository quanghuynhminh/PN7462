==============================================================================
                         NXP Semiconductors
                    PN7462AU FW and SW Examples
                  PN7462AU Customer Demo Board v2.2           
                            v05.07.01
                  PN7462AU HAL version  4.11.0.2
                        
                            Readme.txt
==============================================================================

Table of Contents
_________________

1 Document Purpose
2 Description of the package
3 Restrictions
4 Configurations
5 Package Contents
6 Mandatory materials (not included)
7 Hardware Configuration
8 Software Configuration
9 Steps to follow
10 List of supported NFC Reader Boards/ICs



1 Document Purpose
==================

  This document describes the content of the PN7462AU Product Support Package 
  as well, known problems and restrictions.


2 Description of the package
============================
  
  Package contains PN7462 FW, PSP examples and documentation required to start 
  working with PN7462AU.


3 Restrictions
==============

  - SW examples are prepared and tested to be run on the PN7462B Customer Demo 
    board.
  
  
4 Configurations 
================

  - The Software can be compiled Cortex M0 based PN7462AU from NXP.
  
  
5 Package Content
=================

  - EULA.pdf (EULA - End User License Agreement)
  
  - FreeRTOS-License.txt (License agreement of the FreeRTOS component)

  - Readme.txt (this document)

  - .\PN7462AU Documentation\...
      + Folder contains all available documents to work with PN7462AU Customer 
        Demo board and relevant documents for development.
      - "UM10957 - PN7462AU Door Access User Manual.pdf" 
      - "UM10951 - PN7462AU POS User Manual.pdf" 
      - "UM10915 - PN7462AU PC CCID Reader User Manual.pdf" 
      - "UM10913 - PN7462AU Software User Manual.pdf" 
      - "UM10883 - PN7462AU Quick Start Guide - Customer Board.pdf" 
      - "UM10858 - PN7462AU Hardware user manual.pdf" 
      - "AN11784 - PN7462AU How to integrate RTOS.pdf" 
      - "AN11738 - PN7462AU Contact Application.pdf" 
      - "AN11706 - PN7462AU Antenna design guide.pdf" 
      - "AN11785 - PN7462AU LPCD and Standby mode.pdf" 
      - "AN11868 - PN7462AU - Integration with SWD Downloaders.pdf" 
      - "AN3703 - PN7462AU_IAR_Integration.pdf" 
    - "UM10948 - PN7462 EEPROM Management.pdf" 
  
  - .\PN7462AU Datasheet\...
      + Folder contains the PN7462AU and PN736X Datasheet
        - PN736X.pdf 
        - PN7462.pdf 

  - .\PN7462AU FW and SW Examples\...
      + Folder contains the PN7462AU FW source code and SW examples provided to support PN7462AU
      - Keil IDE plugin
      - IAR IDE plugin
      - MCUXpresso IDE plugin
      - LpcFw_phExHif
      - LpcFw_phExPos
    


6 Mandatory materials (not included)
====================================
  
  - MCUXpresso IDE as described on the the web site:
    http://www.nxp.com/mcuxpresso
    
  - LPC-Link 2
    extensible, stand-alone debug probe 
    [http://www.nxp.com/products/reference-designs/lpc-link2:OM13054] 
    
    
7 Hardware Configuration
========================

  Before starting this application, HW Changes may be required for the used
  board.  Refer to the following User Manuals / Application notes before
  starting with this example.

  - UM10883: PN7462 Quick Start Guide - Customer Board
    + Important: See Section on "Adding PN7462AU Plugin" in that document.
    

8 Software Configuration
========================

  - The Software can be compiled for Cortex M0 based PN7462AU from NXP.
    
    
9 Steps to follow
=================

  This package is distributed with the installer working on the Windows OS.
  After successful installation deliverables of the PN7462 are available on the 
  hard drive:
    - Datasheet
    - Documentation
    - Software

  
  Steps to import SW package in MCUXpresso IDE:

  1) For running this application, connect to the PN7462AU Customer demo board.

  2) Create a new MCUXpresso workspace and import this project and it's
     dependencies:

     NxpNfcRdLib, PN7462AU and FreeRTOS_Library needs to be imported
     
     Note: by default all those projects are imported automatically.

  3) Ensure MCU Type in "Project Properties" --> "C/C++ Build" --> "MCU
     Settings" for this project and its dependencies as listed in Step-2 is
     set Correctly:

     For PN7462AU: PN74xxxx --> PN7462AU-C3-00

     Note: by default all projects are configured to PN7462.

  4) Ensure Build Configuration for this project is selected correctly.
     Where allowed, set the build configuration of dependent projects also.

     For PN7462AU: DebugPN7462AU / ReleasePN7462AU

  5) Please ensure that ph_NxpBuild_App.h is updated as per the selection of
     the IC and Platform.

     e.g. For LPC1769, NXPBUILD__PH_LPC1769 needs to be enabled, and
     NXPBUILD__PH_LPC11U68, NXPBUILD__PHHAL_HW_PN7462AU, etc. needs to be
     disabled.  Similarly, for NXPBUILD__PHHAL_HW_PN5180,
     NXPBUILD__PHHAL_HW_PN7462AU, NXPBUILD__PHHAL_HW_RC523 needs to be
     disabled.  Similar change is needed when switching to other supported
     Board/IC as listed in Section-10

  6) Build the project.

  7) Start the "Debug" session of IDE which will first flash the executable
     and start the task.

  8) When this application is running on the target MCU setup and when you
     bring the NFC cards or phone in proximity, the example application will
     detect and reports the NFC technology types detected.


10 List of supported NFC Reader Boards/ICs
==========================================

  1) PN7462AU Customer Evaluation Board

  ---------------------------------------------------------------------------

  For updates of this example, see
  [http://www.nxp.com/pages/:NFC-READER-LIBRARY]    
    

11. Revision History
====================
05.07.01
- PN7462 iAR and Keil project are updated

05.07.00
- PN5180 HAL Optimization
    HAL Exchange Optimization:
    HAL PN5180 was optimized to reduce EMVCo Transaction time by reducing number
    of BAL Exchanges with PN5180 FE which are not required for EMVCo Transaction.
    Inventory Read and Inventory Page Read Error:
    When multiple SLIX (ISO15693) card are placed in the field, PN5180 fails to detect 
    the collision when Inventory Read and Inventory Page Read commands are sent, 
    as PN5180 returns Timeout instead of Collision error.
    HAL PN5180 error check logic is changed to give preference to Collision error over Integrity error.
    Poll Guard Time Optimization:
    Poll guard time optimization was done in NFC Reader Library generically to meet 
    EMVCo Poll guard time requirement on different platforms (Host Microcontroller + NXP FE’s)
    with constant guard time values. As the Poll guard time was made constant across Platforms,
    when PN5180 is used in Linux environment with i.MX6-UL or similar controller, 
    EMVCo Poll guard time test cases are inconsistent.
    Instead of using CLIF timer, DAL timer is used to wait for Poll guard time to expire before sending Poll command.
- Discovery Loop
    EMVCo polling loop is optimized by moving generic code that needs to be executed first time, 
    instead of executing in a loop. Also, the FDT of HLTA is been considered while configuring GTB before sending WupB command.
- PAL 15693 FDT configuration did not consider the ASK configuration of HAL. 
    PAL 15693 is now updated to configure FDT based on the ASK configuration of HAL as per ISO15693 Specification.

05.02.01
 - USB Supend mode updated
 - EEPROM building scripts updated

05.02.00
– OSAL update
    OSAL can now be used as an independent library and is not coupled with NFC
    Reader Library, which enables the use of OSAL in systems which may or may not
    use NFC Reader Library. If any other system (ex: mPOS, Secure Card Reader)
    where NFC Reader Library is optional and is using OSAL for OS abstraction, then
    there is no overhead in the integration of NFC Reader Library within the system.
    After OSAL changes, if the customer needs to port NFC Reader Library on any other
    RTOS or different different controller then NFC Reader Library does not need to be
    changed any more but only changes are required in OSAL which is outside NFC Reader 
    Library which makes porting easier than before without the need of changing 
    NFC Reader Library code base.
– DAL (Driver Abstraction Layer):   
    DAL provides API’s to abstract Microcontroller GPIO functionalities like configuring
    a pin to input/output/interrupt, reading and writing to pins. DAL also provides generic
    BAL abstraction layer required for NFC Reader Library.
    If NFC Reader Library needs to be ported on any other Host Microcontroller or
    Microcontroller SDK then NFC Reader Library need not be changed but changes are
    only required to be done in DAL.
- PN5180 Digital Delay:
    NFC Reader Library PN5180 HAL will read the FW version of PN5180 during HAL
    initialization and uses this FW version information to either apply digital delay inside
    HAL of NFC Reader Library or PN5180 FW.
    On PN5180 firmwrae version 3.6 and below the digital delay is applied by host software
    (NFC Reader Library), on firmware version 3.8 and newer the digital delay is applied by
    PN5180 firmware.
- AL ICode component updated
- AL ICode DNA component added
- Type 5 Tag support updated
- Polling guard time setting fixed

4.06.00
- CLRC663 (plus) - Low Power Card Detection (LPCD) improvements
  Additional options are provided to configure different I/Q thresholds when LPCD Filter
  is enabled to choose either between stable detection with power saving (Option1) or higher detection range (Option2).
- Antenna related configuration for CLRC663 (plus) is moved into separate header file
- ISO18000-3 mode 3 (Icode-ILT) tag detection improved (CLRC663 (plus) only).

v04.05.30:
  - NFC Reader Library update
  - updated documents
    
  to previous version v04.05.00:
     - new PN7462AU FW: "PN7462AU-FW_v04.050.03_20161010-Extended.zip"
     - updated documents
    
  to previous version v04.03.02:
     - new PN7462AU FW: "PN7462AU-FW_v04.05.00_20161010-Extended.zip"
     - updated documents
     
    