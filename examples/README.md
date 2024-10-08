## Device Tree overlay examples for sunxi devices

These are some example overlays for the niche devices (i.e. IIO sensors), custom sensor boards with multiple devices on them or devices that require customization by end user (i.e. SPI displays and touch screens)

Compared to the other ones in this repository these are "standalone" - no fixup script is required, so they can be used with the configfs interface too.


#### double-spidev-bus.dts
- overlay for 2 SPIdev devices on 2 different SPI controllers
- may require activating the SPI buses by a kernel provided overlay (i.e. `overlays=spi0 spi1`) to set pin muxing and bus aliases


#### double-spidev-hw-cs.dts / double-spidev-sw-cs.dts
- overlay for 2 SPIdev devices on 1 SPI bus
- may require activating the SPI bus by a kernel provided overlay (i.e. `overlays=spi0`) to set pin muxing and bus aliases
- requires using SPI bus that supports multiple chip selects (including software/GPIO based ones)
- requires `spi-add-cs1` overlay on H3 and H5


#### spi-ili9341-tft.dts
- overlay for driving the ili9341 connected to the SPI bus based around the 2.4 inch Linksprite
display
- bindings documentation: [ili9341.yaml](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/tree/Documentation/devicetree/bindings/display/panel/ilitek,ili9341.yaml)
- Although written for this display it can easily be customised to work with any ili9341 driven
display, simple change the height and width parameters to suite your particular display


#### gpio-button.dts
- overlay for a GPIO button, active low (when connected to GND), using either EINT capable GPIO pin or polling
- bindings documentation: [gpio-keys.txt](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/tree/Documentation/devicetree/bindings/input/gpio-keys.txt), [gpio-keys-polled.txt](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/tree/Documentation/devicetree/bindings/input/gpio-keys-polled.txt)
- internal pull-up is optional and not recommended unless using short wires
- requires adding `poll-interval` property if using "gpio-keys-polled" driver


#### i2c-ad799x.dts
- overlay for the adc breakout board for the Pcduino based around the ad799x connected to the
I2C bus
- bindings documentation: [ad799x.yaml](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/tree/Documentation/devicetree/bindings/iio/adc/adi,ad799x.yaml)
- may require activating the I2C bus by a kernel provided overlay (i.e. `overlays=i2c1`) to set pin muxing
- may require add a voltage reference 'vref', depending on the particular chip used


#### i2c-apds9960.dts
- overlay for an apds9960 sensor connected to the I2C bus
- bindings documentation: [apds9960.txt](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/tree/Documentation/devicetree/bindings/iio/light/apds9960.txt)
- may require activating the I2C bus by a kernel provided overlay (i.e. `overlays=i2c1`) to set pin muxing
- may require changing the interrupt GPIO specifier
- using external pull-up resistor on the interrupt line is highly recommended if the module doesn't have one


#### i2c-edt-ft5x06.dts
- overlay for a touch screen connected to the I2C bus
- bindings documentation: [edt-ft5x06.txt](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/tree/Documentation/devicetree/bindings/input/touchscreen/edt-ft5x06.txt)
- may require activating the I2C bus by a kernel provided overlay (i.e. `overlays=i2c1`) to set pin muxing
- may require changing the `compatible` property value even though currently it's not required
- may require changing or removing wake and reset GPIOs
- may require changing the interrupt GPIO specifier


#### i2c-ina219.dts
- overlay for a INA219 current shunt and power monitor connected to the I2C bus
- bindings documentation: [ina2xx.txt](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/tree/Documentation/devicetree/bindings/hwmon/ina2xx.txt)
- may require activating the I2C bus by a kernel provided overlay (i.e. `overlays=i2c1`) to set pin muxing
- may require changing the `compatible` property value
- may require changing the `reg` property value to the actual address of the chip
- may require changing the `shunt-resistor` depending on board resistor


#### i2c-pca857x.dts
- overlay for a PCA8574 GPIO/interrupt controller connected to the I2C bus
- bindings documentation: [gpio-pcf857x.txt](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/tree/Documentation/devicetree/bindings/gpio/gpio-pcf857x.txt)
- may require activating the I2C bus by a kernel provided overlay (i.e. `overlays=i2c0`) to set pin muxing
- may require changing the `compatible` property value
- may require changing the `reg` property value to the actual address of the chip
- may require changing the interrupt GPIO specifier

#### i2c-pca9685.dts
- overlay for the NXP PCA9685 I2C PWM controller connected to the I2C bus
- bindings documentation: [pca9685-pwm.txt](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/tree/Documentation/devicetree/bindings/pwm/nxp,pca9685-pwm.txt)
- may require activating the I2C bus by a kernel provided overlay (i.e. `overlays=i2c0`) to set pin muxing
- may require changing the `reg` property value to the actual address of the chip


#### sht1x.dts
- overlay for a Sensirion SHT1x sensor connected to 2 GPIO lines
- bindings documentation: [sht15.txt](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/tree/Documentation/devicetree/bindings/hwmon/sht15.txt)


#### spi-ads7846.dts
- overlay for an ADS7846 touch screen connected to the SPI0 controller on H3 based board
- bindings documentation: [ads7846.txt](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/tree/Documentation/devicetree/bindings/input/touchscreen/ads7846.txt)
- may require activating the SPI bus by a kernel provided overlay (i.e. `overlays=spi0`) to set pin muxing
- may require changing the `compatible` property value even though currently it's not required
- may require adding wake GPIO
- may require changing the interrupt GPIO specifier


### spi-enc28j60
- overlays for a ENC28J60 Ethernet controller connected to the SPI bus
- bindings documentation: [microchip,enc28j60.txt](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/tree/Documentation/devicetree/bindings/net/microchip,enc28j60.txt)
- may require activating the SPI bus by a kernel provided overlay (i.e. `overlays=spi0`) to set pin muxing
- may require changing the interrupt GPIO specifier
- using external pull-up resistor on the interrupt line is highly recommended if the module doesn't have one


### spi-mcp251x
- overlays for a MCP251x CAN controller connected to the SPI bus
- bindings documentation: [microchip,mcp251x.txt](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/tree/Documentation/devicetree/bindings/net/can/microchip,mcp251x.txt)
- may require activating the SPI bus by a kernel provided overlay (i.e. `overlays=spi0`) to set pin muxing
- may require changing the `compatible` property value
- may require changing the interrupt GPIO specifier
- may require changing the clock frequency to an actual value of the onboard resonator
- using external pull-up resistor on the interrupt line is highly recommended if the module doesn't have one
