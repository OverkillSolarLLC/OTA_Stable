# OTA_Stable

# Pathfinder BMS firmware change log July 31 2025
## V_0.301_STABLE
- New feature: BLE encryption can be disabled via OLED . Improves Android device compatibility. 
 - bug fix: incorrect calculation of current calibration %.
 - bug fix: long press on reset puts the BQ76952 to sleep. Added a partial reset on every reboot.
 - bug fix: MQTT: SOC, capacity, confidence mapped to the wrong variables.
## V_0.300_STABLE
Note- This version was shipped with a few units but replaced by V0.301 before publishing OTA.
 -  New feature: selectable SOC tracking algorithms.
  	- Simplified learning cycle
 -  Enabled the Serial API on the UART port in addition to the USB port. (Also published the API documentation, see github.com/OverkillSolarLLC/documentation)
 - New feature: Customizable .CSV formatted streaming logs on UART and USB ports.
 - New feature: Click "always ask" to un-reject a previously rejected OTA update.
 - New feature: Raw coulomb counter with OLED monitoring screen.

 - bug fix: unable to set short circuit parameter to max value.
 - bug fix: report lot code correctly
 - bug fix: Some of the event counts were mapped to the wrong values.
 - bug fix: NTC1 events not incrementing event count.
 - bug fix: turn on fault led for NTC1 events.
 - bug fix: enable OCD3 protection (L1 DSG Overcurrent)
 - bug fix: L1 & L2 Fault recovery time mapped to wrong register.

## V_0.222_BETA
 - Bug fix: Prevent learning cycle instructions from repeating after the cycle is finished.
 - Added Learning cycle "Stage" to non-volatile storage. When the BMS reboots after this update, the stage variable will be lost, but thereafter it will be retained. This does not interrupt the Learning cycle but it will interrupt the sequencing of the on-screen instructions if a learning cycle is already active.
 - 
## V_0.221_BETA
 - Bug fix: disabling radio power freezes the user interface
 - Don't auto-start the Learning cycle. Added _Start Learning Cycle button_ to Learning Cycle screen.
 - Changed _Charge Overcurrent Recovery_ parameter default to -200mA from 0mA to prevent rapid cycling of a charge overcurrent fault. (not user adjustable)
 - Bug fix: changing protection parameters to overlap an existing fault condition caused the BQ76952 to crash. Added a partial reset of the BQ76952 after every parameter change.


## V_0.215_BETA
Note: some BMSs were shipped with V_0.215_BETA, but the OTA and UF2 files were bumped up to V_0.221_BETA before publishing the update.
### Learning cycle 
- Adjusted learn cycle termination voltages to narrower range to accommodate moderate cell mismatch. These parameters are still non adjustable in the field.    
- Added _Learning Cycle Reset_ function to the RESET screen. This resets the BQ43Z100 and re-initializes the learning cycle. User parameters are not overwritten, but calibrations are erased. Null current calibration must be repeated after a learning cycle reset.   
- Added a warning when changing design capacity after learning cycle is started. Once started, the Z100 learning cycle must be reset before capacity can be changed. 
- Bug fix: Energy and current not scaled correctly for the learning cycle. This caused the reported measured capacity to be 5x too high. Scale factor for energy and current is now calculated when setting Design Energy. Current resolution will now change depending on the scale factor.    
- Improved on screen instructions for learning cycle.

### MQTT
 - Add MQTT status screen.
 - Bug fix: MQTT was not indexing active cells if less than 16. High/low cell numbers were off by 1.
 - Bug fix: Cell delta incorrectly formatted for MQTT
 - Limit the retry rate for a disconnected MQTT broker to 5 minutes, or 5 seconds if the user cancels the warning popup.
 - Bug fix: MQTT broker disconnecting may cause OTA to fail due to memory leak. MQTT not properly handling broker disconnect events.
 - Bug fix: MQTT leaking memory during connect attempts if radio power is off.
 - Bug fix: MQTT power was displaying current instead of power due to wrong data variable- linked the correct data source.

### Recovery Mode
- Added Recovery Mode screen- Recovery mode is manual operation only, hold the OK button to engage the output via the predischarge circuit.

### Misc
- Added indicators around cell voltage on OLED cell voltage screens to show which cell is balancing.    
- Added function to load alpha OTA with secret code (UP-DN-L-R). Customers should not use this function unless asked to test a specific alpha build.     
- Display RemainingCapacity on SOH screen.      
- Bug fix: Idle calibration routine was overshooting and not getting fresh data during automatic calibration.     
- Bug fix: Wifi scan failed if radio power disabled. Added a warning and prevent starting the scan.    
- Bug fix: Antenna light sometimes stuck on when radio power is disabled.   
- Bug fix: restart BLE advertising after cycling radio power.


### V_0.129_BETA 

Initial release, shipped with all Pathfinder BMSs from lot 1

