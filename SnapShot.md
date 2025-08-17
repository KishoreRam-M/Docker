# 🖼 What is a **Snapshot** in Virtualization?

👉 **Definition:**
A **snapshot** is like a **photo of your VM at a point in time** (including disk, memory, and settings).

If something goes wrong later, you can **“go back”** to that exact state.

---

## 📌 Example:

* You have a VM with Ubuntu + Python installed.
* You take a snapshot (📸).
* Then you install Node.js and MySQL.
* If MySQL setup breaks → you just **revert** to the snapshot (Ubuntu + Python only).

---

## 🎯 Why useful?

* **Testing software** – try updates safely.
* **Safe experiments** – break things, then roll back.
* **Quick backup** – faster than full backup.

---

## 💡 Analogy:

Imagine you’re playing a video game 🎮.

* Before fighting the boss, you **save game** (snapshot).
* If you lose, you just **reload the save** instead of restarting the whole game.

---

✅ **One-liner:**
A **snapshot** = a savepoint of your VM that lets you roll back to an earlier state anytime.
