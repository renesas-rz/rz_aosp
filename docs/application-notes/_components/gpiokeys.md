## **GPIO Keys (Power, Volume up/down)**

AOSP now supports GPIO key events for **USER_SW1 (Power button)**, **USER_SW2 (Volume down button)**, and **USER_SW3 (Volume up button)**. These buttons are integrated with the standard Android input framework and can generate key events for application and system-level handling.

**Supported Features**

- Single press detection for Power and Volume up/down buttons.

- Double press detection for Power.

- Long press detection for Power.

- Combined key detection for two-button presses (Power + Volume up, Power + Volume down).

