# wireless-mouse-hardware-teardown
  > Hands-on teardown and reverse engineering of a wireless mouse to study its embedded hardware, PCB architecture, electronic components, optical sensor, RF communication, power management, and working principle.
wireless mouse works
> 
![Image](https://images.openai.com/static-rsc-4/9bPrhveaa8mkyAbVwfq_6ECaidir3ok6oP-0rFnFxjKQBeog_M4PFB7k45gngbNSw6URFVbhqgSujVReg61Fk02JUeVicL1NLL3lmjHuMGxWDGd09KQgIW9XX7LiOX6VpUIFGBnCyMKId1JiYRbOQW7pnT3X7i2tc-ReJPazhgG5k0tW5ZNQyLwp31-h0CjZ?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/pK_Lr_xskkt-d16SYfwNWSLRnmoABSFjdnySRWEQuUqbLyYWzs-vuKAxraFxD486jii59wtN1dN1N2L_0nn9SKyLIzQyM6b7c_UdKqjU6-qeVSsicXYb3-BhUuJkdTg1s0TvW44xwMxYF3uReGkCorJj_Os_tQqMAnR-wnMSh1-7u6eUYo2iOYZRxSq3Plbm?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/IdOY8EFfw0vqJiGqoG9VsfjAa4QlK7d7zOO3MCPPUK2FJkwqqJSaL0mslJXqy2CZWMZsvd4R0tN1cnMC2mk_pDXg-RPcsDgaIhNmfvadFqLpfeo2Iz-OGtywNNu-MF6ZfZHQuoYYuPrBJWpOL7-a7aZ1YPxVXN_gD0a0nJpZKTskbs-mk3Je-UXCyLLxLPuI?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/9mcE1W8Aq98DKDKXTAivb7fqYQGdlwPbDZQAC4pwwhnaeIUnk7nDM3KMyH2uOoRMjISHw1o-pOWQtGJNsuw_-AG8MyGp2Fxcmrt2W48TMv40YeVyxdgmLLwqkyiYqShqay7JaDEDYSXZeuTxkXHUXCIdkLv4gZTBFOIsds9hLtTZqSaGaAZTUwZawlbUwhXP?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/vy-EJYZHB2LrZLtyr783QM_R7PyZjEUYYiZJuoIwHR2lX86SH81AJ2QQ5OB1IZV3vqg9ksKqfW-uk4lZGExbWsmb35kVLvlvOBUnIRCubj2FbJDjYEXgG6RkCno8_Gr_B66P07_nWApi_fPoFgHQoPgSm56TKjL4lDA974OrXgjVlYoCYIEmEMYh65SigJRd?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/Ljz-HAWOA346MvwZJkImA-lqjTcEvmTZvk765lkq3h4yqt3RGa7681NeJ-RPEoU1ad_1FWvOpOAh2-p1Cp6P8-u0NmHmy6ohERNb9swQuYxfDGwfGL3x6Dbsu6VNzTGzi7CDkaTmr1xX8Ht-ozjkCXJ3o7yELjbbuCJX1T1w5KvX0FT5vndZ8SbPqq3nML2L?purpose=fullsize)

### 🖱️ Wireless mouse: complete flow

```text
        DESK SURFACE
             ↓
       LED / IR light
             ↓
       Optical Sensor
             ↓
     Motion Processor
             ↓
      Microcontroller
             ↓
     2.4 GHz / Bluetooth
             ↓
     USB Receiver / PC
             ↓
        Cursor moves
```

### 1. The sensor detects movement

Under the mouse is a tiny **optical sensor**.

It takes thousands of images of the desk surface every second.

When you move the mouse:

```text
Before movement:   [texture pattern]
After movement:       [texture pattern]
                         →→→
```

The sensor calculates the change in **X and Y direction**.

### 2. The microcontroller processes it

A small MCU inside the mouse receives data such as:

```text
X = +12
Y = -5
Left button = 0
Right button = 1
Scroll = 0
```

It packages this into a mouse data packet.

### 3. Wireless transmission

The mouse then transmits those packets using either:

**2.4 GHz RF**
or
**Bluetooth**

For a typical 2.4 GHz mouse:

```text
Mouse
  │
  │ 2.4 GHz RF
  ↓
USB Receiver
  ↓
Computer
```

The USB receiver acts as the bridge between the wireless mouse and the computer.

### 4. The computer receives the packet

The computer's operating system receives something like:

```text
Movement:
X = +12
Y = -5

Button:
Left = 0
Right = 1
```

It converts that into cursor movement.

### 🔋 Where does the battery come in?

The battery powers:

* Optical sensor
* LED/IR emitter
* MCU
* RF/Bluetooth chip
* Buttons/encoder

That's why wireless mice need batteries or rechargeable cells.

### 🔥 The interesting part

A wireless mouse is actually a **small embedded system**:

**Sensor + optics + MCU + RF communication + power management + firmware**

So if you're interested in **Embedded Systems + Wireless Networking**, a wireless mouse is a very good simple example of how all these components work together.

If you want, I can also explain **the actual 2.4 GHz wireless communication inside a mouse packet-by-packet**, from the sensor all the way to the laptop.

A computer mouse detects movement using a **sensor underneath the mouse**. The exact method depends on whether it is an **optical** or **laser** mouse.

### 🖱️ How an optical mouse works

![Image](https://images.openai.com/static-rsc-4/nJg1J1CbabQcBFyyEceYpanIEhhCR8hRB-sFSr9eo9zzdg0wUhj4AQnTV-bdWWQZyuD3WjbZlqchkoDWFq0x9OTxCzy4uIWoGbTxRbLPygzh6cNWMQM5ZWMH01fj9DfJWbeXaJghF_QT32uzgv7yoD2ic1XU5KvON7Mfgt7yFm4KA-MwtyU5RpzBfWv8TvRa?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/ZummGKnvW6qLeatpZAvFcC9vW87IuLUNcQYi18hGDRz56XWspZGELvAUsWIj3PBIfU2z_0z1-WA6DaTfdUh9aYmVIhxlb_ui4pBdBLmT16e7-fWsz04UqXiTyr3eV1pSvUYAKt5A9IN-ASEEYphMVkRDbtHeSMEnerELc-3vqO-dG8CbQagfwu951fQrAiFN?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/im7Pi2xbuyTurkcphUmK6RqiNKKJP4TQzH2U2Taj-YszyX4oEreRGeXYSmCo55KdQ0k3YAVtCYkuHTVwsBbu0jPKkt4G9FVW_TuMqxek_f8hsy-Y5YMbJLOrtgvRuIvrGDYk9JXAAxoRLdBnbpvd-LzOKRItPu6yT4yaiDcWL-M1rnHzI_0a_lp-oAd6aFTF?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/QnWbyS6ZXmHLaeFkEU-Nelf9oPIKdlSefWdKSSbpzsgVwzidxyBnCd4Dbl9YDPHzDnkf4-Vnk-pL1AU71hGnHCiUMZBcnpwHDoyVN7OZvi5fjAHqgFurn6u0t7pvR_PoGMR-xZ76hnUc0f_mPbhUVKHc6bphFTy9-G2rq8Rvh8MOw-f0s2laAKkGK8DdPZ11?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/ODd4ScGKPGhxpXXE9iZt9YhSN3grW870eoNQIPOc2Uru10rONodZa07fo0Gn95YhrY6dcR4tx93P1kJlFu2wbhB8sydXPCFbZlCiAObAGKycon4JpebIsQYjsQAlwO-HBING6CirL0NSIV-DzF1169UvzVnFWxHL9uNwfmkMC8awkuecd1hX78C4sIcn3iIM?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/DqA1EdNf0kDW-LqM9iIS3FQFD5EbF5apincmhsiRIYaKU6X3ck8tvapszJnm9wnfmRaB3NqDOlhWosvdFUnnxXXzfVMDfJByG5R5QNmW6KMHg5wwNHxrOCWPwnve2voz7CZHeGlfqkiJ_ToqNGXNRVYs-LBIA-itg8D2pBahM4tLTXM_0zD4gHtvvkuG2yXE?purpose=fullsize)

Think of the mouse as a **tiny camera + computer** looking at your desk thousands of times per second.

**Step 1 — Light illuminates the surface**
An LED shines light onto the desk/mousepad.

**Step 2 — Tiny camera captures the surface**
A small CMOS image sensor takes many tiny pictures of the surface.

**Step 3 — The mouse compares pictures**
Suppose the first image contains:

`A B C D`

After you move the mouse right, the next image might look like:

`    A B C D`

The sensor recognizes that the texture has shifted.

**Step 4 — The processor calculates movement**
A tiny processor inside the mouse calculates:

* ΔX → left/right movement
* ΔY → forward/backward movement

**Step 5 — It sends the data to the computer**
The mouse sends this information through **USB or Bluetooth/wireless**.

The computer then converts the movement into the cursor movement you see on screen.

### 🔬 What is actually inside?

A modern optical mouse typically contains:

**LED → Lens → Surface → Image Sensor → DSP/Processor → USB/Wireless Controller → Computer**

The interesting part is the **image sensor + DSP**.

It doesn't need to understand the entire picture. It looks for changes in the surface pattern and determines how far that pattern moved.

### 🖱️ What about the buttons and scroll wheel?

The mouse also has separate sensors/switches:

* **Left/right buttons:** mechanical or optical switches detect clicks.
* **Scroll wheel:** an encoder detects rotation and direction.
* **DPI button:** changes how much cursor movement is produced for a given physical movement.

### ⚡ Why does the mouse work without a mouse ball?

Old mechanical mice used a **rubber ball**.

The ball physically rotated two encoder wheels:

**Ball → X wheel + Y wheel → electrical pulses → computer**

Modern optical mice replaced that mechanical system with:

**Light → camera → image processing → movement data**




wireless-mouse-hardware-teardown/
│
├── README.md
├── images/
│   ├── mouse-exterior.jpg
│   ├── pcb-front.jpg
│   ├── pcb-back.jpg
│   ├── microcontroller.jpg
│   ├── rf-section.jpg
│   ├── sensor.jpg
│   ├── power-section.jpg
│   └── teardown-process.jpg
│
├── documentation/
│   ├── components.md
│   ├── pcb-analysis.md
│   └── working-principle.md
│
└── LICENSE
```


**1. Project Title**

> # Wireless Mouse – Hardware Teardown & Analysis

**2. About**


> This project documents the teardown, hardware analysis, and reassembly of a wireless mouse to understand its internal embedded electronics, PCB architecture, wireless communication, optical sensing, power management, and overall working principle.

**3. Objectives**

* Understand the internal architecture of a wireless mouse
* Identify major electronic components
* Analyze the PCB and circuit sections
* Understand optical motion sensing
* Study wireless communication architecture
* Understand power management
* Document the teardown and reassembly process

**4. Hardware Components**

* Microcontroller / SoC
* RF transceiver
* Optical sensor
* Crystal oscillator
* Voltage regulator
* Capacitors & resistors
* Switches
* LED
* Battery contacts
* USB receiver interface

**5. Working Principle**

Simple block diagram:

```text
Mouse Movement
      ↓
Optical Sensor
      ↓
Microcontroller
      ↓
RF Transmitter
      ↓
Wireless Receiver
      ↓
Computer
```

**6. PCB Analysis**

**7. Teardown Process**

Step 1 → Outer casing
Step 2 → Battery compartment
Step 3 → PCB removal
Step 4 → Component identification
Step 5 → PCB analysis
Step 6 → Reassembly
Step 7 → Functional testing

**8. Key Learnings**

* Basic PCB architecture
* Embedded controller identification
* RF communication architecture
* Optical sensing mechanism
* Power distribution
* PCB component identification
* Hardware troubleshooting
* Safe teardown and reassembly





