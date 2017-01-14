I was really disappointed my Trezor didn't work out-of-the-box with Electrum on Tails. I believe it's in the pipeline for the next major release of Tails, but not sure when that will be. That doesn't do me any good today, and I really don't want to use my Trezor outside of Tails if I can avoid it.

I couldn't find any guides or posts that walked through how to do it, so I figured it out. These instructions are good today, which for me is Tails 2.9.1, Electrum 2.7.17, and python-trezor 0.7.6-1.

# Getting It to Work
1. Launch Tails with root capabilities. Optionally enable persistence to keep from having to repeat some (all?) of these steps.
2. Use a root terminal to install the `python-trezor` package. This is a library Electrum needs to talk to the Trezor. There may be a way to do this through the package manager GUI, but I am unsure. You have to install from the unstable branch `sid` since `python-trezor` is not in the stable branch. These are the commands I used:

        sudo apt-get update
        sudo apt-get -t sid install python-trezor

3. Install the udev rules for Trezor devices. This makes the Trezor's name under `/dev` consistent, which I believe assists with Electrum finding it. This can be found at https://raw.githubusercontent.com/trezor/trezor-common/master/udev/51-trezor.rules. I used the following command:
    
        sudo wget -O /etc/udev/rules.d/51-trezor.rules https://raw.githubusercontent.com/trezor/trezor-common/master/udev/51-trezor.rules

3. Get the latest Electrum source for Linux from Electrum.org. This is needed because I don't think the included version of Electrum with Tails works with the latest `python-trezor` library or the latest Trezor devices. For me the download name was `Electrum-2.7.17.tar.gz`.
4. Unpack the archive. From the download directory I used `tar xzf Electrum-2.7.17.tar.gz` but extracting it via the GUI should be fine too.
5. Plug in your Trezor.
6. Launch electrum from the terminal by entering the `Electrum-2.7.17` directory step 4 created and using this command:

        python electrum -P

7. Select "standard wallet" and "hardware device", at which point it should detect the Trezor you plugged in. If not, kill Electrum and try again. Maybe try unplugging and plugging in the Trezor in before relaunching. I did have this segfault before, or not detect the Trezor, but relaunching/replugging worked afterward.
8. Walk through the setup, which will have you type in a PIN on the Trezor, maybe a password, and then an account number (default 0).
9. Configure your Electrum settings for access via the tor network (the default new settings for Electrum tries to connect without Tor, which won't work under Tails)

  > Tools -> Network -> Select "SOCKS5" for Proxy, localhost, 9050.

10. Configure the rest of your Electrum settings as needed and use Electrum per normal.

# Regarding Persistence (Keeping it Working)
**For steps 4-5, 8-11 (Electrum):** Because you passed the `-P` flag launching electrum in step 6, your wallet and settings are stored in the `electrum_data` directory of `Electrum-2.7.17`. As long as you launch with `python electrum -P` from the `Electrum-2.7.17` directory, that's where it will look for those settings. So if you want to keep from having to download and set up Electrum again, you can just keep the `Electrum-2.7.17` directory (probably in your home folder if you've enabled persistence?).

**For step 2 (python-trezor):** Tails persistence has an option to keep around installed packages ("APT Packages" and "APT Lists"), which might allow you to keep python-trezor. I haven't tested this. I am a little uncertain since the install uses the unstable branch.

**For step 3 (udev rule):** I'm relatively certain the udev rule will get wiped every time (I can't imagine why it'd be included with persistence), so perhaps you should just keep a copy and remember to copy it each time. Sort of a bummer.

# Improvements
I'd like to hear from anyone regarding improving or testing this process, specifically:

 - Easier ways to accomplish the above (maybe someone will write a script?).
 - Keeping everything persistent so that you don't have to repeat any of these steps and could sign transactions from an offline computer if needed.
 - More secure methods of performing the steps above to keep from introducing unnecessary risk to your Tails machine / install or Electrum application/wallet.
 - If updates (to Tails, Electrum, python-trezor, or any dependencies) breaks this process and how to work around it.
