# micropytimer

Micropython friendly library to create timers that trigger functions

# Overview

This package implements a simple timer functionality for both python and micropython. Timers trigger a user defined function when they expire. Timers can be set to expire either at an interval after they start or at a fixed expiration time. Useful for triggering an action after a period of in action, checking for updates to some state, of causing actions to happen at fixed times of day.

Timers come in two types: Long and Short. Long timers have intervals in seconds or expirations in seconds since the beginning of the epoch. Short timers only work under micropython, and have intervals in microseconds. Fixed expirations are trickier for short timers, since the time is measured since the last time the device clock turned over. Regardless of the timer type, the functions for using them (``setup_timer``, ``start_timer``, etc.) are common to both.

By default, timers are one-shot. If a looping timer is needed, the the function that the timer triggers should include a call to the ``start_timer`` function.

# Installation

``pip install micropytimer``

# Example Setup

Examples of how to set up and use timers are shown in the ``example.py`` and ``example_util.py`` files included with the packing on GitHub, here. Of note the timers should not be instantiated directly. For the functionality to work properly they need to be added to the library's ``timer_registry`` it needs to be created with the ``setup_timer`` function.

# Timer Definitions

Each timer is set up with a name and dictionary that contains all of its attributes. The possible attributes are:

* action: The function to be executed when the timer expires.

* args: Arguments to be passed to the function defined by action

* is_set: Whether the timer is set when it is defined. Timers that are not set are not checked. A timer can be set at any time after it is defined using the ``start_timer()`` function

* long: Whether the timer in question is a long timer with its interval measured in seconds. If not the timer is short, with an interval in milliseconds. Note that short timers only work under micropython.

+ interval: The number of seconds or millisecons after starting when the timer will fire. Will override expiration

* expiration: A fixed clock time in seconds since epoch start when the timer will fire. Will not be used of interval is also given.

# Library Functions

All setup and interaction with timers should be done through the following functions.

``check_timers``

``setup_timer``

``start_timer``

``stop_timer``

``trigger_timer``

``override_timer_expiration``

``force_restart``

``show_timers``
