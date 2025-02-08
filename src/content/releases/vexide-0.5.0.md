---
title: vexide 0.5.0
project: vexide
date: 2024-11-28
---

vexide 0.5.0 is our biggest update of all time. We focused on hopefully finalizing all of our device APIs in this update and on improving the quality of our documentation.
We highly recommend reading [our Thanksgiving blog post](/blog/posts/thanksgiving-update-24/) for more info.

## Added

- You can now detect controller release occurrences with `ButtonState::is_now_released`.
- Added support for 5.5W motors with a new constructor (`Motor::new_exp`) and four new getters (`Motor::max_voltage`, `Motor::motor_type`, `Motor::is_v5`, and `Motor::is_exp`) for `Motor`. ([#167](https://github.com/vexide/vexide/pull/167))
- Added support for the V5 Workcell Electromagnet smart device. ([#176](https://github.com/vexide/vexide/pull/176))
- The conditions upon which functions return errors are now documented. ([#155](https://github.com/vexide/vexide/pull/155)).
- Implemented the `Copy` trait for `BannerTheme`.
- Added a getter that retrieves a `Controller`'s identifier. ([#189](https://github.com/vexide/vexide/pull/189))
- Added support for controllers in `DynamicPeripherals`. ([#196](https://github.com/vexide/vexide/pull/196))
- Added the ability to return Smart Ports, ADI ports, the display, and controllers to `DynamicPeripherals`. ([#196](https://github.com/vexide/vexide/pull/196))
- Added a `SmartDevice::UPDATE_INTERVAL` constant for all devices, representing the amount of time between data updates from a given device. ([#199](https://github.com/vexide/vexide/pull/199)) (**Breaking Change**)
- Added a `toggle` method to `AdiDigitalOut` to toggle between level outputs (210).
- Added the `OpticalSensor::GESTURE_UPDATE_INTERVAL` (50mS) constant ([#211](https://github.com/vexide/vexide/pull/211)).
- Added a `toggle` method to `AdiDigitalOut` to toggle between level outputs.
- Added a `SerialPort::set_baud_rate` method for the adjusting baudrate of a generic serial smartport after initialization. ([#217](https://github.com/vexide/vexide/pull/217))
- Added fields containing relevant failure information to several error types ([#221](https://github.com/vexide/vexide/pull/221)) (**Breaking Change**)
- Added support for the power button in the `Controller` API. ([#231](https://github.com/vexide/vexide/pull/231)) (**Breaking Change**)
- Added implementations of `Mul<i64>` and `Div<i64>` for `Position`, allowing
  for opaque scaling ([#230](https://github.com/vexide/vexide/pull/230))
- Added panic hook support comparable to the Rust standard library through `vexide::panic::set_hook` and `vexide::panic::take_hook` ([#234](https://github.com/vexide/vexide/pull/234))
- Added support for legacy ADI servos through the `AdiServo` API. ([#241](https://github.com/vexide/vexide/pull/241))
- Added support for the V5 AI Vision Sensor ([#58](https://github.com/vexide/vexide/pull/58))
- Added FOV constants to the Vision Sensor ([#58](https://github.com/vexide/vexide/pull/58))
- Added missing `Send` and `Sync` `impl`s for RwLock. ([#239](https://github.com/vexide/vexide/pull/239))
- Added the `Proportional` font family and support for fractional font scaling. ([#248](https://github.com/vexide/vexide/pull/248)) (**Breaking Change**)
- Added `AdiDigitalOut::with_initial_state` to set the initial state of a digital output while creating it ([#246](https://github.com/vexide/vexide/pull/246))
- Added `Display::draw_text` to write `Text` to a `Display`. ([#247](https://github.com/vexide/vexide/pull/247))
- Added support for the legacy Yaw Rate Gyroscope through the `AdiGyroscope` struct. ([#236](https://github.com/vexide/vexide/pull/236))
- Added support for reading/writing to the Brain's SDCard slot using the `vexide::core::fs` module. ([#22](https://github.com/vexide/vexide/pull/22))

## Fixed

- `AdiAddrLed::set_pixel` will now correctly return an error if the device's ADI expander is disconnected. ([#155](https://github.com/vexide/vexide/pull/155))
- The `dbg!();` now works as expected when no arguments are supplied to it. ([#175](https://github.com/vexide/vexide/pull/175))
- `Motor::velocity` now correctly returns the estimated velocity instead of target velocity. ([#184](https://github.com/vexide/vexide/pull/184)) (**Breaking Change**)
- Removed useless generics from `AdiAddrLed::new`. ([#197](https://github.com/vexide/vexide/pull/197)) (**Breaking Change**)
- IMU calibration timeouts should no longer appear when the IMU is in working condition. ([#212](https://github.com/vexide/vexide/pull/212))
- Fixed an issue preventing ADI updates in fast loops. ([#210](https://github.com/vexide/vexide/pull/210))
- `Motor::status` can now actually return the `MotorStatus::BUSY` flag. ([#211](https://github.com/vexide/vexide/pull/211))
- Fixed a memory leak on every `RadioLink` construction. ([#220](https://github.com/vexide/vexide/pull/220))
- Fixed a panic in `RadioLink::open` that would occur if a program using a VEXlink radio was ran twice. ([#243](https://github.com/vexide/vexide/pull/243))
- Fixed a bug with IMU reset offsets being applied incorrectly. ([#242](https://github.com/vexide/vexide/pull/242))

## Changed

- Controller state is now returned all at once to reduce error checking. ([#152](https://github.com/vexide/vexide/pull/152)) (**Breaking Change**)
- Controller bumper naming scheme has been changed from `<left/right>_trigger_<1/2>` to `button_<r/l><1/2>`. ([#204](https://github.com/vexide/vexide/pull/204)) (**Breaking Change**)
- `Button::was_pressed` has been renamed to `ButtonState::is_now_pressed`.
- `battery::capacity` now returns from 0.0-1.0 rather than 0-100.
- `battery::voltage` is now returned in volts rather than millivolts.
- `battery::current` is now returned in amps rather than milliamps.
- Changed the incorrect return types of `AdiSolenoid::is_open` and `AdiSolenoid::is_closed` from `LogicLevel` to `bool`. ([#164](https://github.com/vexide/vexide/pull/164)) (**Breaking Change**)
- Renamed `Motor::MAX_VOLTAGE` to `Motor::V5_MAX_VOLTAGE` and added `Motor::EXP_MAX_VOLTAGE`. ([#167](https://github.com/vexide/vexide/pull/167)) (**Breaking Change**)
- Moved the ability to convert Smart devices to `SmartPorts` out of the `SmartDevice` trait and into the devices themselves. ([#171](https://github.com/vexide/vexide/pull/171)) (**Breaking Change**)
- Renamed `SmartDeviceType::Magnet` to `SmartDeviceType::Electromagnet`. ([#176](https://github.com/vexide/vexide/pull/176)) (**Breaking Change**)
- Getters and constructors will now create warnings when their return values are not used. ([#155](https://github.com/vexide/vexide/pull/155))
- Renamed `OpticalSensor::rgb` to `OpticalSensor::color` and `OpticalSensor::raw` to `OpticalSensor::raw_color` ([#179](https://github.com/vexide/vexide/pull/179)) (**Breaking Change**).
- Made the following functions infallible: `AdiAccelerometer::sensitivity`, `AdiAccelerometer::max_acceleration`, `AdiPotentiometer::potentiometer_type`, `AdiPotentiometer::max_angle`, `Motor::target`, and `RotationSensor::direction`. ([#182](https://github.com/vexide/vexide/pull/182)) (**Breaking Change**)
- `OpticalSensor::led_brightness` now returns a number from `0.0` - `1.0` rather than a number from `1` - `100`. ([#155](https://github.com/vexide/vexide/pull/155)) (**Breaking Change**)
- Renamed `Motor::update_profiled_velocity` to `Motor::set_profiled_velocity`. ([#155](https://github.com/vexide/vexide/pull/155)) (**Breaking Change**)
- `Mutex` is now `?Sized`, matching the behavior of the standard library. ([#202](https://github.com/vexide/vexide/pull/202)) (**Breaking Change**)
- Switched to the [`rgb`](https://crates.io/crates/rgb) for color storage. `vexide::devices::color` is now `vexide::devices::rgb` which re-exports the `Rgb` type. ([#201](https://github.com/vexide/vexide/pull/201)) (**Breaking Change**)
- Renamed `AddrledError::Adi` to `AddrledError::Port`. ([#203](https://github.com/vexide/vexide/pull/203)) (**Breaking Change**)
- Renamed `GpsImu::set_data_rate` to `GpsImu::set_data_interval`. ([#199](https://github.com/vexide/vexide/pull/199)) (**Breaking Change**)
- Renamed `InertialSensor::set_data_rate` to `InertialSensor::set_data_interval`. ([#199](https://github.com/vexide/vexide/pull/199)) (**Breaking Change**)
- Renamed `Motor::DATA_WRITE_INTERVAL` to `Motor::WRITE_INTERVAL`. ([#199](https://github.com/vexide/vexide/pull/199)) (**Breaking Change**)
- Renamed `InertialSensor::accel` to `InertialSensor::acceleration` ([#213](https://github.com/vexide/vexide/pull/213)) (**Breaking Change**)
- Renamed `GpsImu::accel` to `GpsImu::acceleration` ([#211](https://github.com/vexide/vexide/pull/211)) (**Breaking Change**)
- `SerialPort::read_byte` now takes `&mut self`. ([#215](https://github.com/vexide/vexide/pull/215)) (**Breaking Change**)
- `OpticalSensor::last_gesture` now returns an `Option<Gesture>` if no gesture was detected. ([#215](https://github.com/vexide/vexide/pull/215)) (**Breaking Change**)
- The `time` field on `Gesture` is now returned as an instance of `SmartDeviceTimestamp`. ([#215](https://github.com/vexide/vexide/pull/215)) (**Breaking Change**)
- `Gesture` and `GestureDirection` no longer implements `Default`. ([#215](https://github.com/vexide/vexide/pull/215)) (**Breaking Change**)
- Renamed `vexide::devices::geometry` to `vexide::devices::math`. ([#218](https://github.com/vexide/vexide/pull/218)) (**Breaking Change**)
- Replaced the custom `Point2` type with `mint`'s `Point2` type for better interop. ([#218](https://github.com/vexide/vexide/pull/218)) (**Breaking Change**)
- `SmartPort::device_type` now returns an `Option<SmartDeviceType>` which returns `None` if no device is connected or configured to a port. ([#219](https://github.com/vexide/vexide/pull/219)) (**Breaking Change**)
- Renamed the `LinkError::NonTerminatingNul` and `ControllerError::NonTerminatingNul` variants to simply `Nul` and added a source error. ([#220](https://github.com/vexide/vexide/pull/220)) (**Breaking Change**)
- Made `ControllerScreen` methods and `Controller::rumble` asynchronous and added synchronous `try_<action>` variants. ([#222](https://github.com/vexide/vexide/pull/222)) (**Breaking Change**)
- Renamed `ControllerScreen::MAX_LINE_LENGTH` to `ControllerScreen::MAX_COLUMNS`. ([#222](https://github.com/vexide/vexide/pull/222)) (**Breaking Change**)
- Refactored `InertialCalibrateFuture` to an opaque wrapper over the internal state machine. ([#225](https://github.com/vexide/vexide/pull/225)) (**Breaking Change**)
- `GpsSensor::new` is now infallible and no longer returns a `Result`. ([#240](https://github.com/vexide/vexide/pull/240)) (**Breaking Change**)
- `RadioLink::new` can now only fail on `NulError` and will not bail if a radio is disconnected. ([#240](https://github.com/vexide/vexide/pull/240)) (**Breaking Change**)
- `RadioLink::unread_bytes` can now return a `LinkError::ReadError`. ([#243](https://github.com/vexide/vexide/pull/243))
- `RadioLink::is_linked` is now infallible. ([#243](https://github.com/vexide/vexide/pull/243)) (**Breaking Change**)

## Removed

- Removed `Motor::DATA_READ_INTERVAL`. Use `Motor::UPDATE_INTERVAL` instead. ([#199](https://github.com/vexide/vexide/pull/199)) (**Breaking Change**)
- Removed `InertialSensor::CALIBRATION_TIMEOUT` and replaced it with the `InertialSensor::CALIBRATION_START_TIMEOUT` and `InertialSensor::CALIBRATION_START_TIMEOUT` constants. ([#212](https://github.com/vexide/vexide/pull/212)) (**Breaking Change**)
- `AdiDigitalOut::level` now reads the actual reported level value from VEXos, and thus now returns a `Result`. ([#210](https://github.com/vexide/vexide/pull/210)) (**Breaking Change**)
- Removed the defunct `usd` module from `vexide::devices`. ([#198](https://github.com/vexide/vexide/pull/198)) (**Breaking Change**)
- Removed `AdiSolenoid`. Use `AdiDigitalOut` instead. ([#210](https://github.com/vexide/vexide/pull/210)) (**Breaking Change**)
- Removed the deprecated `ZERO_POSITION` and `ZERO_VELOCITY` `Motor` status flags. ([#211](https://github.com/vexide/vexide/pull/211)) (**Breaking Change**)
- `GestureDirection::None` has been removed, as `OpticalSensor::next_gesture` now returns an `Option<Gesture>`. ([#215](https://github.com/vexide/vexide/pull/215)) (**Breaking Change**)
- `GestureDirection` no longer has a `From` conversion for `u32`. ([#215](https://github.com/vexide/vexide/pull/215)) (**Breaking Change**)
- Removed the `nalgebra` feature. All math types should natively support nalgebra conversions without any additional features. ([#218](https://github.com/vexide/vexide/pull/218)) (**Breaking Change**)
- Removed `SmartDeviceType::None`. `SmartPort::device_type` now returns an `Option<SmartDeviceType>` which serves the same purpose. ([#219](https://github.com/vexide/vexide/pull/219)) (**Breaking Change**)
- Removed `Position`-to-`Position` `Mul`/`Div` ops, as they were mathematically unsound. Prefer using `Position`-to-scalar operations for this. ([#237](https://github.com/vexide/vexide/pull/237)) (**Breaking Change**)
- Removed `LinkError::Nul`. ([#240](https://github.com/vexide/vexide/pull/240)) (**Breaking Change**)
- Removed `LinkError::Port`, because it was broken. VEXlink will no longer perform port validation. ([#243](https://github.com/vexide/vexide/pull/243)) (**Breaking Change**)
- Removed the `TextSize` enum. Use the associated constants on the new `FontSize` struct instead. ([#248](https://github.com/vexide/vexide/pull/248)) (**Breaking Change**)

## New Contributors

[@zabackary](https://github.com/zabackary) made their first contribution in #164!
