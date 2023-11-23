# MAC Address Changer
Using Python and Kali Linux to build a simple MAC address changer

<body>
  <h1>Tutorial: Using Python and Kali Linux to Build Basic MAC Address Changer</h1>
  <p>In this tutorial, we'll build a simple MAC address changer in Kali Linux using Python. We'll use the <code>subprocess</code> and <code>argparse</code> modules to build two functions that allow users to change a device's MAC address directly in the Linux terminal using custom commands.</p>
  <img src="https://github.com/amaraphi/mac_address_changer/assets/144752187/dfdad23d-8d6a-451e-b371-4fd23ec97e3d"/>

  <p>To complete this tutorial you'll need to have Kali Linux installed as well as an IDE. In this case, I've used Pycharm Community Edition. (Follow this tutorial for instructions on installing Pycharm on Kali Linux.)</p>
  <h1>Step 1: Creating a function that changes the MAC address</h1>
  <p>Log in to Kali Linux.</p>
  <p>Open the Linux terminal. Find the names of your devices's interfaces by using <code>ifconfig</code>.
    <img src="https://github.com/amaraphi/mac_address_changer/assets/144752187/f2e3d0a9-92f8-4868-a1e2-e86b573b173c"/>
  <p>Open Pycharm (or any IDE of your choice) and create a new project. Create a new Python file.</p>
  <p>Import the <code>subprocess</code> module.</p>
  <p>Create a new function, <code>change_mac</code>, that accepts two parameters: the name of the interface and its new MAC address:</p>
  <p><code>def change_mac(interface, mac_address):</code></p>
  <p>Use the <code>subprocess.call()</code> method to execute system commands using a list with the following syntax:</p>
  
  ``` 
subprocess.call(["ifconfig", interface, "down"])
subprocess.call(["ifconfig", interface, "hw", "ether", mac_address])
subprocess.call(["iconfig", interface, "up"])
```
  <h1>Step 2: Creating a function that accepts user arguments in the Linux command line</h1>
  <p>Import the <code>argparse</code> module. This allows users to use custom Linux commands to change the MAC address directly in the terminal.</p>
  <p>Define a new function named <code>user_arguments()</code>.</p>
  <p>Create an <code>OptionParser()</code> object.</p>

  ```
parser = OptionParser()
```

  <p>Use the <code>add_argument()</code> method to create custom user arguments for the interface name and the new MAC address using the following syntax:</p>

```
parser.add_argument("-i", "--interface", dest="interface", help="Name of interface with new MAC address")
parser.add_argument("-m", "--mac_address", dest="mac_address", help="New MAC address to be entered")
parser.parse_args()
```
  <p>The <code>parse_args()</code> method captures the user input, which can be represented with the variable <code>values:</code></p>

```
values = parser.parse_args()
```
  <p>These individual values can be accessed this way:</p>

```
interface = values.interface
mac_address = values.mac_address
```
  <p>Using <code>parser.error()</code>, we can now add conditional statements to test if the user has entered valid input. If a user doesn't enter a valid interface name or MAC address, an error message is displayed and the program will terminate.</p>
  <p>If the user has entered valid input the program will return those values to the <code> user_arguments()</code> function when it is called.</p>

```
    if not values.interface:
        parser.error("Please enter a valid interface name.")
    elif not values.mac_address:
        parser.error("Please enter a valid MAC address.")
    return values
```

  <p>Now that the user input is returned to the <code>user_arguments()</code> function, we can call and execute the function in this way:</p>

```
values = user_arguments()
```
  <p>Recall that the <code>change_mac</code> function takes two parameters: <code>interface</code> and <code>mac_address</code>. This function can now be called with the following syntax:</p>

```
  change_mac(values.interface, values.mac_address)
```
  <p>As a final step, we can add a confirmation message when the MAC address has been successfully changed:</p>

```
print("The MAC address for " + interface + " has been successfully changed to: " + mac_address)
```
  <p>The final program will look like this:</p>

```
def user_arguments():
    parser = argparse.OptionParser()
    parser.add_argument("-i", "--interface", dest="interface", help="Name of interface to be changed")
    parser.add_argument("-m", "--mac", dest="mac_address", help="New MAC address")
    values = parser.parse_args()
    if not values.interface:
        parser.error("Please enter a valid interface name.")
    elif not values.mac_address:
        parser.error("Please enter a valid MAC address.")
    return values
def change_mac(interface, mac_address):
    print("The MAC address for " + interface + " has been successfully changed to: " + mac_address)
    subprocess.call(["ifconfig", interface, "down"])
    subprocess.call(["ifconfig", interface, "hw", "ether", mac_address])
    subprocess.call(["ifconfig", interface, "up"])

values = user_arguments()
change_mac(values.interface, values.mac_address)
```
</body>
