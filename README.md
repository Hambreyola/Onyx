# Onyx
Onyx is a minimal, Wayland-native desktop environment designed to feel solid, fast, and complete out of the box — while staying intentionally small and free of feature bloat.

This project is in development.



Documentation (ignore):
1. src/tinywl.c
Language: C
What: Handles logic of the compositor
How: Uses wlroots to talk to host window/hardware
Manages: input handling, rendering, window management

2. meson.build
Language: Meson 
What: Build manager
How: Runs when building compositor, makes instructions for ninja
Manages: dependencies, compiler instructions