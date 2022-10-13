# PAM OTP
## Integrate OTP authentication with any PAM module using [google-authenticator-libpam](https://github.com/google/google-authenticator-libpam).


## Prerequisites
You need the following in order to be able to use PAM OTP:
* python3
* python3-pip
* [argparse](https://pypi.org/project/argparse/)
* [google-authenticator-libpam](https://github.com/google/google-authenticator-libpam) (Your distro package manager is likely to have this)

## Installation
1. Clone this repo and cd into it
```
git clone https://github.com/DaniAsh551/pam-otp
cd pam-otp
```
2. Install the dependencies mentioned in the [Prerequisites](#Prerequisites) and requirements.txt (`pip install -f ./requirements.txt`)
3. Generate your secrets by running `google-authenticator`. Pay attention, answer the questions and note the path where it generates the secret file. (Ususally `~/.google_authenticator`)
4. Run the install script as root. You need to know what these arguments are:
 * secret:  The path to the secret file generated in the previous step
 * control: The control flag to use. See [here](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/managing_smart_cards/pam_configuration_files#pam-control) for details.
 * prefix:  The root/prefix to use, it's a good idea to leave this alone if you are not sure what this is
 * PAM_CONF: The path to the PAM config file where pam-otp should be added to


## Example Scenarios
* Adding OTP to KDE Plasma login on debian stretch:
```
sudo apt update
sudo apt install -y libpam-google-authenticator
git clone https://github.com/DaniAsh551/pam-otp
cd pam-otp
google-authenticator
sudo ./install --secret $HOME/.google_authenticator /etc/pam.d/kde
```
* Adding OTP to OpenSSH on debian stretch (Also make sure UsePAM is set to `yes` in `/etc/ssh/sshd_config`):
```
sudo apt update
sudo apt install -y libpam-google-authenticator
git clone https://github.com/DaniAsh551/pam-otp
cd pam-otp
google-authenticator
sudo ./install --secret $HOME/.google_authenticator /etc/pam.d/sshd
```
