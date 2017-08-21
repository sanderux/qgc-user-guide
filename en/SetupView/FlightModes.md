# Flight Modes Setup

The *Flight Modes* section allows you to map flight modes to radio channel(s), and hence to the switches on your radio control transmitter. Both flight mode setup and the available flight modes are different in PX4 and ArduPilot (and there are some differences between ArduCopter and ArduPlane). 

To access this section, select the **Gear** icon (Vehicle Setup) in the top toolbar and then **Flight Modes** in the sidebar.

> **Note** You must already have [configured your radio](../SetupView/Radio.md) in order to set flight modes.

<span></span>
> **Tip** Flight modes provide different levels of *autopilot-assisted flight*, and *fully autonomous flight* via missions or offboard (API-based) control. Different flight modes allow new users to learn flying with a more forgiving platform than provided by basic RC control alone. They also enable automation of common tasks like taking off, landing and returning to the original launch position.
> <div></div>
> For more information about the flight modes see:
> * [PX4 Flight Modes](https://docs.px4.io/en/flight_modes/)


## PX4 Pro Flight Mode Setup

*PX4* (*QGroundControl*) supports two modes for mapping flight modes to transmitter switches/dials:

- **Single Channel Mode Selection:** Assign up to 6 flight modes to switch positions encoded in a single channel. 
- **Multi Channel Mode Selection:** Assign modes to switch positions encoded in one or more channels. Some modes are hard coded to share channels, or are defined/set automatically based on other mode selections (the behaviour of multi-channel mode selection can sometimes be confusing). 

> **Tip** The recommended approach is use *Single Channel Mode Selection* because it easy to understand and configure.


### Single-Channel Mode

The single-channel selection mode allows you to specify a "mode" channel and select up to 6 flight modes that will be activated based on the PWM value of the channel. You can also separately specify channels for mapping a kill switch, return to launch mode, and offboard mode.

> **Note** In order to use approach you will first need to configure your *transmitter* to encode the physical positions of your mode switch(es) into a single channel. There is a video guide of how this is done for the popular *Taranis* transmitter [below](#taranis_setup) (check your documentation if you use a different transmitter). 

To configure single-channel flight mode selection:

1. Turn on your RC transmitter.
1. Select the **Gear** icon (Vehicle Setup) in the top toolbar and then **Flight Modes** in the sidebar.
   
   ![Flight modes multi-channel](../../images/setup/flight_modes_single_channel_px4.jpg)
   
   > **Tip** If the screen opens in *Multi Channel Mode* click the **Use Single Channel Mode Selection** button to change screen.
   
1. Specify *Flight Mode Settings*:
   * Select the **Mode channel** (above this shown as Channel 5, but this will depend on your transmitter configuration). 
   * Select up to six **Flight Modes**.
1. Specify *Switch Settings*:
   * Select channels for *Return To Launch* mode, *Kill Switch*, and *offboard* mode (if you have spare switches and channels on your transmitter).
1. Test that the modes are mapped to the right transmitter switches:
   * Check the *Channel Monitor* to confirm that the expected channel is changed by each switch.
   * Select each mode switch on your transmitter in turn, and check that the desired flight mode is activated (the text turns yellow on *QGroundControl* for the active mode).

All values are automatically saved as they are changed.




### Multi-Channel Mode

> **Tip** We recommend you use [Single Channel Flight Mode](#single_channel) selection because the Multi Channel selection user interface can be confusing. If you do choose to use this method, then the best approach is to start assigning channels and take note of information displayed by *QGroundControl* following your selection. 

The multi-channel selection UI allows you to map one or more modes to one or more channels. There are some modes (and hence switches) that must always be defined, and the channel to which they must be allocated.

To configure flight modes using the multi-channel UI:

1. Turn on your RC transmitter.
1. Select the **Gear** icon (Vehicle Setup) in the top toolbar and then **Flight Modes** in the sidebar.
   
   ![Flight modes multi-channel](../../images/setup/flight_modes_multi_channel_px4.jpg)
   
   > **Tip** If the screen opens in *Single Channel Mode* click the **Use Multi Channel Mode Selection** button to change screen.
   
1. Select the modes you want to assign to your switches and select the associated channel (selected modes will *move* in the UI to be grouped by channel).
   There are a number of complications on the mode to channel assignments:
   * Some modes will have a grayed out channel selector because they cannot be disabled and you cannot directly set the value. For example:
     * *Mission* mode - Has the same channel number as *Hold* (if it is defined), or otherwise the same channel as *Stabilized/Main* mode.
     * *Altitude* mode - Has the same channel number as *Position Control* (if it is defined), or otherwise the same channel as *Stabilized/Main* mode.
   * *Assist* mode -  This mode is added to the same channel as *Stabilized/Main* mode if (and only if) *Position Control* is enabled and defined on a different channel than *Stabilized/Main*.
1. Click the **Generate Thresholds** button. 
   * This will automatically create threshold values for all modes, spread evenly across each channel for its assigned modes. For example, in the mode assignment shown above, most modes are assigned to mode 5, and you can see that the channel thresholds for each mode are spread evenly across the channel. 


> **Note** This flight mode selection mechanism is relatively complicated due to the way that PX4 works out which mode should be selected. You may be able to gain some insight from this [flow chart](https://dev.px4.io/en/concept/flight_modes.html#flight-mode-evaluation-diagram) (PX4 Developer Guide).


