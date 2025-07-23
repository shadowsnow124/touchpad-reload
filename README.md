# HP Zorin OS Touchpad Reload Script (Post-Suspend Fix)

## 💡 Problem

laptop users face an issue where their touchpad stops responding after the laptop wakes up from sleep (suspension). This script provides an automated solution.

## ✅ Tested Environment

* **Laptop Model:** HP ENVY X360
* **Operating System:** Zorin OS 17.3 Core

While tested on this specific setup, this solution might work for other Laptop or Linux distributions experiencing similar touchpad issues after suspend.

## ⚙️ How It Works

The core problem is that the touchpad's driver (specifically `i2c_hid_acpi` for many laptops) sometimes fails to re-initialize properly after the system resumes from a low-power state.

The `touchpad-reload` script fixes this by:

1.  **`sudo rmmod i2c_hid_acpi`**: This command **removes** (unloads) the `i2c_hid_acpi` kernel module (your touchpad's driver) from the system's memory.
2.  **`sudo modprobe i2c_hid_acpi`**: This command then **loads** the `i2c_hid_acpi` module back into memory, forcing it to re-initialize and properly detect your touchpad.

The script is placed in a special directory (`/lib/systemd/system-sleep/`) where `systemd` (your system's service manager) automatically runs scripts after a suspend/resume event. Making the script executable (`sudo chmod +x`) allows the system to run it as a program.

## 🚀 Installation (Drop-In Method)

Follow these simple steps to install the touchpad fix:

1.  **Download the Script:**
    Download the `touchpad-reload` file directly from this repository to your laptop.

2.  **Open a Terminal:**
    Press `Ctrl + Alt + T` on your keyboard.

3.  **Move the Script to the System Directory:**
    Place the downloaded `touchpad-reload` file into the correct system directory (`/lib/systemd/system-sleep/`).
    Assuming the file is in your `Downloads` folder, use this command:

    ```bash
    sudo mv ~/Downloads/touchpad-reload /lib/systemd/system-sleep/
    ```

    You will be ask for your root password.
    
    or just

    ```
    xdg-open /lib/systemd/system-sleep
    ```
    and drop a file into it
    

5.  **Make the Script Executable:**
    For the system to run the script, it must have executable permissions. In the terminal, run:

    ```bash
    sudo chmod +x /lib/systemd/system-sleep/touchpad-reload
    ```


6.  **Reboot Your System:**
    It's recommended to reboot your laptop to ensure it working properly simply type on termial

    ```bash
    sudo reboot
    ```

    than you good to go
    
7.  **Test the Fix:** (optinal)
    After rebooting and logging in, put your laptop to sleep (e.g., close the lid or select "Suspend"). Then, wake it up. Your touchpad should now work as normal.

## 🗑️ Uninstallation

To remove the fix, simply delete the script file:

1.  **Open a Terminal:** `Ctrl + Alt + T`
2.  **Delete the script:**
    ```bash
    sudo rm /lib/systemd/system-sleep/touchpad-reload
    ```
    Enter your password when prompted.

    or

    ```
    xdg-open /lib/systemd/system-sleep/
    ```

    and delete a `tourchpad-reload` file and that it 
## ⚠️ Disclaimer

This script involves modifying system files. While designed to be safe and effective, use it at your own risk. Always ensure you have backups of important data.

## 🤝 Contribution & Feedback

If this script helped you, please consider starring this repository!
If you have any feedback, questions, or discover that this solution works on other laptop models or distributions, feel free to open an issue or reach out.

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
