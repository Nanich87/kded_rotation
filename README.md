# kded_rotation

KDED module for handling automatic screen rotation on X11, with visual feedback before orientation change happens. Some assembly might be required.

# Installation

Run `./install_kded_rotation.sh` and install missing dependencies as needed. To start the service, you will need to restart your current session or reboot.

You'll most likely need `qt5-qtbase-devel`, `cmake-utils`, `extra-cmake-modules`, `iio-sensor-proxy`, `xrandr`, `qt5-qtsensors` and `kf5-kded-devel`. Depending on your distribution, these packages might have different names. CMake will tell you which packages it is missing.

On kubuntu run `sudo aptitude install build-essential cmake extra-cmake-modules libqt5sensors5-dev kded5-dev`

# Usage

`orientation-helper` is where the actual screen rotation happens. This is achieved by calling `xrandr --rotation $value`, which works in most circumstances. You can adjust `orientation-helper` to fit your setup and reinstall to apply.

To reduce or increase the timer before the rotation happens, adjust `timer.start(25);` in `screenrotator.cpp`:

```cpp
void ScreenRotator::startProgress() {
	if (progress == -1) {
		timer.start(25);
		progress = 0;
	}
}
```
If your touchscreen does not change orientation, you can show your input devices with `xinput list` and copy the name of your touchscreen controller, then edit `/usr/bin/orientation-helper` (or type `whereis orientation-helper` to get the right path)

```
IS_TOUCH=$(echo $props | grep -i 'name_of_your_touch_controller_here')
```
save and restart the session to apply.
