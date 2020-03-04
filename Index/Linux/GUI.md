# GUI

---

**To disable GUI on boot, run:**

    sudo systemctl set-default multi-user.target

**To enable GUI again issue the command:**

    sudo systemctl set-default graphical.target

**To start Gnome session on a system without a current GUI just execute:**

    sudo systemctl start gdm3.service