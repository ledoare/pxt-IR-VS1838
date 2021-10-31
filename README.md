# MakeCode extension for Emakefun Motorbit 1.0
# Infrared receptor with a slim NEC compatible IR remote

[![Build Status](https://travis-ci.org/1010Technologies/pxt-makerbit-ir-receiver.svg?branch=master)](https://travis-ci.org/1010Technologies/pxt-makerbit-ir-receiver)
* Based on <b>1010Technologies/pxt-makerbit-ir-receiver</b>
------------------


| ![](https://github.com/ledoare/pxt-motorbit-IR/raw/master/irController.png) | ![](https://github.com/ledoare/pxt-motorbit-IR/raw/master/motorbit.png) |
| :----------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------: |
|                                            _Télécommande Mini Remote_                                            |                                   _MotorBit_                                   |



# IR Remote Receiver Module and Controller Kit

MakeCode extension for set of IR receiver VS1838B HX1838 and Mini Slim controller (product name can vary depending on the seller - see pictures bellow).
Kit usually includes 5mm IR LED for construction of your own transmiter.

## IR Receiver VS1838B HX1838

| ![IR Receiver VS1838B HX1838](https://github.com/BrickHackers/pxt-IR-VS1838/raw/master/irReceiverUnsoldered.png "IR receiver (unsoldered version)") | ![IR Receiver VS1838B HX1838](https://github.com/BrickHackers/pxt-IR-VS1838/raw/master/irReceiverSoldered.png "IR receiver (soldered version)") |
| :-------------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------: | 
|                                                        _unsoldered components_                                                                      |                                                                    _soldered board_                                                             |

IR receiver chip is focused to use with Arduino and Raspberry Pi, however, works with micor:bit and calliope too.
According to VS1838B datasheet, it features:
* **[ frequency ]**  38 kHz
* **[ working voltage ]**  2.7 – 5.5 V DC
* **[ Receiver Distance ]** 22 – 25 m
* **[ Size ]** 7.4 mm x 6.2 mm x 5.3 mm


| ![IR Controller](https://github.com/BrickHackers/pxt-IR-VS1838/raw/master/irCotnroller.png "IR controller") |
| :---------------------------------------------------------------------------------------------------------: |
| _Mini Slim infrared remote controller_                                                                      |

Some sellers could print their logo on controller, but functionality should be same. 
* **[ buttons ]** 17 function keys; the effective life of 20,000 pressings
* **[ frequency ]** 38 kHz
* **[ effective angle ]** 60°
* **[ transmission distance ]** cca 8 m (specific and surroundings, the receiver sensitivity and other factors)

# Documentation


## Extension for Emakefun Motorbit

    Use MakeCode to program your Microbit+Motorbit -> https://makecode.microbit.org/
    
    On your MakeCode Project :
    - click on Menu : Advanced / Extensions
    
    - search for https://github.com/ledoare/pxt-motorbit-IR
    to install infrared receiver extension
    
    - search for https://github.com/emakefun/pxt-motorbit
    to install main Motorbit extension

## Mini Remote IR codes

* (1)-162
* (2)-98
* (3)-226
* (4)-34
* (5)-2
* (6)-194
* (7)-224
* (8)-168
* (9)-144
* (0)-152
* (*)-104
* (#)-176
* (up)-24
* (down)-74
* (left)-16
* (right)-90
* (ok)-56

## makerbit.connectIrReceiver

Connects to the IR receiver module at the specified pin.
<p><b>On Emakefun Motorbit, onboard IR receiver is assigned to pin P1.</b>
but you can plug any other IR receiver on another pin </p> 

```sig
makerbit.connectIrReceiver(DigitalPin.P1, IrProtocol.NEC)
```


### Parameters

- `pin` - digital pin with an attached IR receiver

## irVS1838.connectIrReceiverVisual

Connects to the IR receiver module at the specified pin. Display it on LED matrix.
[ NOTE ] Display animation take some time. This function was added for log pin during testing.

```sig
irVS1838.connectIrReceiverVisual(DigitalPin.P0)
```

### Parameters

- `pin` - digital pin with an attached IR receiver

## irVS1838.onIrButton

Do something when a specific button is pressed or released on the remote control.

```sig
irVS1838.onIrButton(IrButton.Ok, IrButtonAction.Pressed, () => {})
```

### Parameters

- `button` - the button to be checked
- `action`- the trigger action
- `handler` - body code to run when the event is raised

## irVS1838.irButton

Returns the code of the IR button that was pressed last. Returns -1 (IrButton.Any) if no button has been pressed yet.

```sig
irVS1838.irButton()
```

## irVS1838.onIrDatagram

Do something when a specific button is pressed or released on the remote control.

```sig
irVS1838.onIrDatagram(() => {})
```

### Parameters

- `handler` - body code to run when the event is raised

## irVS1838.irDatagram

Returns the IR datagram as 32-bit hexadecimal string. The last received datagram is returned or "0x00000000" if no data has been received yet.

```sig
irVS1838.irDatagram()
```

## irVS1838.wasIrDataReceived

Returns true if any IR data was received since the last call of this function. False otherwise.

```sig
irVS1838.wasIrDataReceived();
```

## irVS1838.irButtonCode

Returns the command code of a specific IR button.

```sig
irVS1838.irButtonCode(IrButton.Num9)
```

### Parameters

- `button` - the button

## MakeCode Example

```blocks

irVS1838.connectIrReceiver(DigitalPin.P0)

basic.forever(function () {
    if (irVS1838.wasAnyIrButtonPressed()) {
        basic.showNumber(irVS1838.irButton())
    }
})

irVS1838.onIrButton(IrButton.OK, IrButtonAction.Pressed, function () {
    basic.showIcon(IconNames.Heart)
})

irVS1838.onIrButton(IrButton.OK, IrButtonAction.Released, function () {
    basic.showIcon(IconNames.SmallHeart)
})

```

## License

Licensed under the MIT License (MIT). See LICENSE file for more details.

## Supported targets

- for PXT/microbit
- for PXT/calliope
