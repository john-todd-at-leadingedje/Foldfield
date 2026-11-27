# Foldfield

Quest 2 VR viewer for classic **PDB** protein structures (wireframe, ball-and-stick, surface later). **Classic PDB only** for now — no mmCIF / PDBx, no AlphaFold workflows.

**Repo:** [john-todd-at-leadingedje/Foldfield](https://github.com/john-todd-at-leadingedje/Foldfield)

---

## Status

- **M0 — XR shell smoke-test:** done (standalone Quest build; test cube visible in headset).
- **Next — M1:** classic PDB load + ball-and-stick + two-hand rotate/scale.

---

## Prerequisites

1. **Unity Hub**
2. **Unity 6 LTS** (e.g. **6000.0.8f1**) with modules:
   - **Android Build Support**
   - **OpenJDK**
   - **Android SDK & NDK Tools**
3. **Meta Quest 2** with **Developer Mode** enabled
4. **Meta Horizon** app on the companion phone (for Developer Mode / device management)

---

## One-time project setup

### 1. Create / open the Unity project

- Unity Hub → **New project** → **3D (URP)**  
  Location parent: `C:\Users\john.todd\source\repos\` · name: `Foldfield`  
  (or open the existing folder at that path)
- Do **not** commit `Library/`, `Temp/`, `Obj/`, `Build/`, `Logs/`.

### 2. Meta XR SDK (v209 All-in-One)

- **Window → Package Manager** → **+ → Add package by name** → `com.meta.xr.sdk.all`  
  (Meta XR All-in-One / Meta XR SDK — pin/use the **v209** line that installs with that package.)
- If **Meta XR Simulator** fails to install, **skip it**. Not required for Quest device smoke-test.
- **Meta App ID / Data Use Checkup (DUC)** are **optional** for the first on-device smoke-test. Add later when Platform features need them.

### 3. XR Plug-in Management (Android / Quest)

- **Edit → Project Settings → XR Plug-in Management**
- Open the **Android** tab (not Desktop alone)
- Enable **OpenXR**
- Enable the **Meta XR** feature group on that Android tab when it appears
- If OpenXR validation complains: enable **Hand Tracking Subsystem** (or the Meta hand-tracking feature the validator names)
- Add **Meta Quest Touch** interaction profiles for controllers when configuring OpenXR features

### 4. Player / package identity

- Package name: `com.leadingedje.foldfield`
- Prefer **IL2CPP**, **ARM64**, Linear color space, URP asset assigned for Android

### 5. Build profile (Unity 6)

Use **File → Build Profiles → Meta Quest** — **not** the old **Build Settings** window.

- Add / select **Meta Quest** → **Enable Platform**

---

## Camera Rig (smoke scene)

1. Open (or create) the boot/smoke scene.
2. **Meta XR SDK → Building Blocks → Camera Rig → Add Block**
3. **Delete or disable** the default **Main Camera** (the Camera Rig provides the XR camera).
4. Add a **Cube** for the smoke-test:
   - Position ≈ `(0, 1.2, 0.8)` or `(0, 1.5, 2)`
   - Scale `1, 1, 1`
   - If the view looks wrong / empty, you may be **inside** the cube — turn around or move the cube farther on **Z**.

---

## Quest device prep

1. Enable **Developer Mode** (Meta Horizon app → headset → Developer Mode).
2. Complete / keep a valid **boundary (Guardian)** so the headset will run apps.
3. USB connect Quest 2 to the PC; allow data / debugging prompts in-headset.
4. If a previous Foldfield install is stuck or won’t update: Quest **Library → All** (or All sources) → uninstall the old app, then rebuild.

---

## Build And Run (smoke-test)

1. Put the headset on (or wake it) so it is an active **Run Device**.
2. **File → Build Profiles → Meta Quest**
3. Confirm the smoke scene is in the **scene list**
4. Select the Quest under **Run Device**
5. Enable **Development Build** (recommended for first deploys)
6. **Build And Run**

Notes:

- An **APK** only appears / installs when the build **Succeeded**. A failure in **~0s** is often **OpenXR validation** — fix the XR Plug-in Management Android tab (OpenXR / Meta / Hand Tracking as required), then rebuild.
- After the app launches **standalone** on the Quest, **USB can be unplugged**.

**Pass:** headset tracking works and the **test cube is visible** in the Quest 2.

---

## Clone / open later

```text
git clone git@github.com:john-todd-at-leadingedje/Foldfield.git C:\Users\john.todd\source\repos\Foldfield
```

Open that folder in Unity Hub with the same Unity 6 LTS editor.

---

## Roadmap (short)

| Milestone | Goal |
|-----------|------|
| **M0** | Repo + XR shell on Quest (**done** — cube smoke-test) |
| **M1** | Classic PDB load, ball-and-stick, polymer/cofactor visibility, two-hand rotate/scale |
| **M2** | Wireframe + surface representations |
| **M3** | Helices / sheets from PDB `HELIX` / `SHEET` |
| **M4** | Import UX polish, reset view, known limits documented |
