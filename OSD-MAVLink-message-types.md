Recommended SRx parameters for Mavlink telemetry:

* SR1_EXT_STAT: (voltage, ampere, satfix, sats) 2Hz
* SR1_EXTRA1: (roll/pitch) 10Hz
* SR1_EXTRA2: (speed) 5Hz
* SR1_POSITION: (GPS heading alt, lat, long) 5Hz

Depending on the serialport used, parameters may also be named SR0_xxx or SR2_xxx. Make sure that the flight control sends out the above telemetry data sets on the appropriate serialport.


The integrated wifibroadcast_osd supports the following Mavlink message types:

#### MAVLINK_MSG_ID_GPS_RAW_INT:

fix = mavlink_msg_gps_raw_int_get_fix_type

sats = mavlink_msg_gps_raw_int_get_satellites_visible


#### MAVLINK_MSG_ID_GLOBAL_POSITION_INT:

heading = mavlink_msg_global_position_int_get_hdg

altitude = mavlink_msg_global_position_int_get_relative_alt

latitude = mavlink_msg_global_position_int_get_lat

longitude = mavlink_msg_global_position_int_get_lon


#### MAVLINK_MSG_ID_ATTITUDE:

roll = mavlink_msg_attitude_get_roll

pitch = mavlink_msg_attitude_get_pitch


#### MAVLINK_MSG_ID_SYS_STATUS:

voltage = mavlink_msg_sys_status_get_voltage_battery

ampere = mavlink_msg_sys_status_get_current_battery


#### MAVLINK_MSG_ID_VFR_HUD:

speed = mavlink_msg_vfr_hud_get_groundspeed

