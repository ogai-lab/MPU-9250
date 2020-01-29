# MPU-9250

The class to control the MPU-9250 to work with python 3.
It works with Raspberry pi 3. Sensor module using the MPU-9250 seems there are a variety of implementation. This class is moving by mounting of strawberry Linux company.

https://strawberry-linux.com/catalog/items?code=12250

## Requirement

You need to make settings to make I2C available in Raspberry pi beforehand.

$ sudo raspi-config

Select menue  "9 Advenced Options” -> “A7 I2C”.
Select "yes" for "Would you like the ARM I2C interface to be enabled?".
Select "yes" for "Would you like the I2C kernel module to be loaded by default?".

next, edit "/boot/config.txt".

$ sudo vi /boot/config.txt

...Add the following contents.
dtparam=i2c_arm=on

Further, edit "/etc/modules"

$ sudo vi /etc/modules

...Add the following contents.
snd-bcm2835
i2c-dev

Restart Raspy after setting.
Confirm that the kernel module is loaded after rebooting.

$ lsmod
...
i2c_dev                 6709  0 
snd_bcm2835            21342  0 
...

python-smbus and i2c-tools are needed.

$ sudo apt-get install i2c-tools python-smbus

Please see the following URL for implementation details.

http://qiita.com/boyaki_machine/items/915f7730c737f2a5cc79

## Usage

$ sudo nice -n -20 python3 mpu9250.py -f 50 -o output_fps50_second10_memory.csv -s 10 -m

* '-f', '--frequency', "Sensor frequency (Hz). (default: 10)", type=int, default=10
* '-o', '--output', "Output filename. (default: output.csv)", default="output.csv"
* '-s', '--second', "Number of seconds recorded. (default: 10)", type=int, default=10
* '-m', '--memory', "Using memory to output data last. (default: false)"
* '--nomag', "No mag. (default: false)"
