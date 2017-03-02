# PCA9534 I/O Expander

PCA9534 GPIO expander library for Particle devices with Particle like API calls. It makes working with PCA9534 I/O expander pins easier, with familiar functions like `pinMode()` and `digitalWrite()`. Refer to the [datasheet](http://www.ti.com/lit/ds/symlink/pca9534.pdf) for more information about the chip.

## Usage

Connect an LED to PCA9534 pin 0 chip, add the PCA9534 library to your project and follow this simple example:

```
#define GPIO_PIN_LED 0

PCA9534 gpio;

void setup() {
  gpio.begin();
  gpio.pinMode(GPIO_PIN_LED, OUTPUT);
}

void loop() {
  gpio.digitalWrite(GPIO_PIN_LED, LOW); // LED On
  delay(500);
  gpio.digitalWrite(GPIO_PIN_LED, HIGH); // LED Off
  delay(500);
}
```

See the examples folder for more details.

## Documentation

### `PCA9534`
Creates a new PCA9534 class to manage a PCA9534 chip.

```
#include "PCA9534.h"
...
...
PCA9534 gpio;
...
...
void setup() {
  gpio.begin();
}
```

### `begin`
Initializes the device and performs initial I2C setup. This method should be called before any others are used.

@param `i2caddr`: sets the slave address of the PCA9534, defaults to 0x20.

```
void setup() {
  gpio.begin(0x20);
}
```

### `pinMode`
Configures the specified pin to behave either as an input, inverted input, or output.

@param `pin`: is number of the pin whose mode you wish to set.

@param `mode`: `INPUT`, `INPUT_INVERTED`, or `OUTPUT`.

```
void setup() {
  gpio.begin();
  gpio.pinMode(0, OUTPUT);
}
```

### `digitalWrite`
Writes a `HIGH` or a `LOW` value to a digital pin.

@param `pin`: is number of the pin whose value you wish to set.

@param `value`: `HIGH`, or `LOW`.

```
void loop() {
  gpio.digitalWrite(0, LOW);
  delay(500);
  gpio.digitalWrite(0, HIGH);
  delay(500);
}
```

### `digitalRead`
Reads the value from a specified digital pin, either `HIGH` or `LOW`.

@param `pin`: is number of the pin whose value you wish to get.

@return the status of the pin either `HIGH` or `LOW`. *Note: when using `INPUT_INVERTED` on `pinMode()`, you will get the inverted status.*

```
void loop() {
  uint8_t buttonStatus = gpio.digitalRead(1);
  if (buttonStatus == HIGH) {
    gpio.digitalWrite(0, LOW); // LED On
  } else {
    gpio.digitalWrite(0, HIGH); // LED Off
  }
}
```

## LICENSE
Copyright 2017 Abdulrahman Saleh Khamis

Licensed under the MIT license