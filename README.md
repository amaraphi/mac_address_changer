# MAC Address Changer
Using Python and Kali Linux to build a simple MAC address changer

<body>
  <h1>Tutorial: Using Python and Kali Linux to Build Basic MAC Address Changer</h1>
  <p>In this tutorial, we'll build a simple MAC address changer in Kali Linux using Python. We'll use the <code>subprocess</code> and <code>argparse</code> modules to build two functions that allow users to change a device's MAC address directly in the Linux terminal using custom commands.</p>
  <p>To complete this tutorial you'll need to have Kali Linux installed as well as an IDE. In this case, I've used Pycharm Community Edition. (Follow this tutorial for instructions on installing Pycharm on Kali Linux.)</p>
  <h1>Step 1: Creating a function that changes the MAC address</h1>
  <p>Log in to Kali Linux.</p>
  <p>Open the Linux terminal. Find the names of your devices's interfaces by using <code>ifconfig</code>.
  <p>Open Pycharm (or any IDE of your choice) and create a new project. Create a new Python file.</p>
  <p>Import the <code>subprocess</code> module</p>
  <p>Create a new function, <code>change_mac</code>, that accepts two parameters: the name of the interface to the changed and its new MAC address:</p>
  <p><code>def change_mac(interface, mac_address):</code></p>
  <p>Use the <code>subprocess.call()</code> method to execute system commands using a list with the following syntax:</p>
  <h1>Step 2: Creating a function that accepts user arguments in the Linux command line</h1>
  <p>Import the <code>argparse</code> module. This allows users to use custom Linux commands to change the MAC address directly in the terminal.</p>
  <p>Define a new function named <code>user_arguments()</code>.</p>
  <p>Create an <code>OptionParser()</code> object, giving it a variable name of your choosing.</p>
  <p>Use the <code>add_argument()</code> method to create custom user arguments for the interface name and the new mac address using the following syntax:</p>
  <p>The <code>parse_args()</code> method captures the user input, which can be represented with the variable values:</p>
  <p>These individual values can be accessed this way:</p>
  <p>Using <code>parser.error()</code>, we can now add conditional statements to test if the user has entered valid input. If a user doesn't enter a valid interface name or MAC address, an error message is displayed and the program will terminate.</p>
  <p>If the user has entered valid input--or values--the program will return those values to the <code> user_arguments()</code> function when it is called.</p>
  <p>Now that the user input is returned to the <code>user_arguments()</code> function, we can call and execute the function in this way:</p>
  <p>Recall that the <code>change_ma</code> function takes two parameters: <code>interface</code> and <code>mac_address</code>. This function can now be called with the following syntax:</p>
  <p><code>change_mac(values.interface, values.mac_address)</code></p>
  <p>As a final step, we can add a confirmation message when the MAC address has been successfully changed:</p>
  <p>The final program will look like this:</p>
</body>
