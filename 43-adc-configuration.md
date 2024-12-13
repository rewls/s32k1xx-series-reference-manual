# Chapter 43 ADC Configuration

## 43.1 Instantiation information

- S32K14x contains two 12-bit ADC modules, ADC0 and ADC1.

### 43.1.1 Number of ADC channels

- Each ADC supports up to 32 external analog input channels, but the exact ADC channel number present on the device is different with packages as indicated in following table.

- For details regarding a specific ADC channel available on a particular package, see Section 4.1 Introduction.

> ##### Table 43-1. ADC external channels per package
>
> |Chip|Package|ADC0|ADC1|
> |-|-|-|-|
> |S32K144|100 LQFP|16|16|

- ADCx_SC1n[ADCH] bit field configurations for a chip are as per the maximum channel configuration for that chip across packages as mentioned in the below table:

> ##### Table 43-2. ADCx_SC1n[ADCH] field configurations
>
> |Chip|ADCx_SC1n[ADCH] range|ADCx_SC1n[ADCH] configuration for module disabled|
> |-|-|-|
> |S32K144|00000 b - 11111 b|11111 b|

- Unavailable channels in a particular package are Reserved for the corresponding package.

> ##### NOTE
>
> - See IO Signal Description Input Multiplexing sheet(s) attached to the Reference Manual for channel details on specific packages.

### 43.1.2 ADC Connections/Channel Assignment

- See IO Signal Description Input Multiplexing sheet(s) attached to the Reference Manual for details on ADC channel connectivity.

- Note that ADCx ADy and ADCx_SEy both refer to Channel y of ADCx.

> ##### Table 43-3. Internal channel availability
>
> |ADC internal channel|ADC0|ADC1|
> |-|-|-|
> |Channel 0|Used for supply monitoring (see ADC internal supply monitoring for detials.)|Reserved|
> |Channel 1|Reserved|Reserved|
> |Channel 2|Reserved|Reserved|
> |Channel 3|Reserved|Reserved|
