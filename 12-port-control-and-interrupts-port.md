# Chapter 12 Port Control and Interrupt (PORT)

## 12.1 Chip-specific PORT information

- Not all pin control settings mentioned in PORT_PCRn register are configurable for all pins.

- Refer 'Bits Configurable' field in 'IO Signal Table' tab of IS Signal Description Input Multiplexing sheet(s) attached to the Reference Manual.

- The bits apart from 'Bit Configurable' fields are reserved and should not be varied from the reset values.

<br>

- PCR bits corresponding to reset pad are non-sticky bits and on a functional reset, reset functionality on this pin will be resumed.

- Prior to entering any ALT functionality, PCR of corresponding pad should be properly configured.

<br>

- On this chip, the pullup and pulldown enables are controllable in analog or disabled pin muxing mode (PORT_PCRn[MUX]=3'b000).

- Before entering Analog mode (ALT0 corresponding to PORT_PCRn[MUX]=3'b000 for corresponding pads for which Analog functionality is available), PUE and PUS should be configured as 0 in corresponding PCR register.

<br>

- PORT_PCRn[PFE] is configurable for only PTA5 and PTD3.

- See IO Signal Description Input Multiplexing sheet(s) attached to the Reference Manual.

- PFE for these should be configured in ALT7 mode only.

- For other modes, PFE should be kept 0.

<br>

- The corresponding PAD should be configured for disabled mode(ALT0) prior to configuring PORT_DFER register.

<br>

- Any pad configuration done in RUN/VLPR mode is retained in low power modes(STOP1, STOP2/VLPS).

<br>

- Wait mode is not supported on this device.

- See Module operation in available power modes for details on available power modes.

### 12.1.1 Number of PCRs

- The number of PCRs for each PORT varies across the products in the S32K1xx and S32K14xW series.

- The following table shows the number of PCRs for each PORT on each product.

- Memory map and register definition documents the superset number of implemented ports.

- PCR registers corresponding to ports which are not present in a particular device are read only 0.

- See the RM attachments IO Signal Description Input Multiplexing sheet(s) for details on the count of PCRs on each product.

> ##### Table 12-1. PCRs on each product
>
> |PORT|S32K144|
> |-|-|
> |PORT A|18|
> |PORT B|18|
> |PORT C|18|
> |PORT D|18|
> |PORT E|17|

### 12.1.2 Finding address for PORTx_PCRn

- For example, in order to write to the PORT register of PTC3 (PTxn), the corresponding mapped register is PORTC_PCR3 (PORTx_PCRn):

    - To find PORTC base address, look up the 'Start address' of "Port C" in "Peripheral Memory Map" tab in the attached S32K1xx_Memory_Map.xls.

        - This is referred henceforth as PORTC_Base_address.

    - To reach PCRn, refer toaddress 'PORTx_Base_address + n * 4d'.

        - For PCR3 of PORTC, this refers to 'PORTC_Base_address + 3 * 4d'.

        - The attachmented IO Signal Description Input Muxing sheet(s) for each device provides the fields available in PCR per PORTx_PCRn (For each PTxn pin) in the tab IO Signal Table.

### 12.1.3 I/O configuration sequence

1. Ensure pins for the peripheral are in tristate state (default out of reset).

2. Initialize peripheral clock in the Peripheral Clock Controller register (PCC) and peripheral specific clocking configurations.

3. Configure the peripheral

4. Initialize port clock for the peripheral pins in the Peripheral Clock Controller register (PCC_PORTx).

5. Configure the peripheral pins mux and features in the Port Control and Interrupts register (PORTx_PCRn).

6. Start communication
