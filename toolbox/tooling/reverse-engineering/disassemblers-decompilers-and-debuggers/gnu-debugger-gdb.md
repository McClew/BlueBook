# GNU Debugger (GDB)

{% hint style="info" %}
## Download & Install

`sudo apt-get install gdb`
{% endhint %}

***

GNU Debugger (GDB) is a reverse engineering tool that enables debugging Linux executable files on the Linux command line.

***

## Cheatsheet

{% tabs %}
{% tab title="Common Commands" %}
<table><thead><tr><th width="162">Command</th><th width="105">Shortcut</th><th>Description</th></tr></thead><tbody><tr><td><code>gdb &#x3C;program></code></td><td>-</td><td>Start GDB with a specific executable.</td></tr><tr><td><code>run</code></td><td><code>r</code></td><td>Start execution of the program.</td></tr><tr><td><code>run &#x3C;args></code></td><td><code>r ...</code></td><td>Run the program with command-line arguments.</td></tr><tr><td><code>quit</code></td><td><code>q</code></td><td>Exit GDB.</td></tr><tr><td><code>kill</code></td><td><code>k</code></td><td>Stop the execution of the program being debugged.</td></tr><tr><td><code>file &#x3C;program></code></td><td>-</td><td>Set the file to be debugged.</td></tr><tr><td><code>info &#x3C;target></code></td><td>-</td><td>provides information in accordance with the given &#x3C;target> parameter. Options include: file, function, breakpoints.</td></tr><tr><td><code>break &#x3C;target></code></td><td><code>b</code></td><td>Sets a breakpoint, the break command can be given an address or a function name as a parameter.</td></tr><tr><td><code>nexti</code></td><td><code>ni</code></td><td>Executes the next single machine instruction, stepping <em>over</em> function calls rather than entering them.</td></tr><tr><td><code>stepi</code></td><td><code>si</code></td><td>Executes exactly one machine instruction, steping into the function call, stopping at the first instruction of the called function.</td></tr></tbody></table>
{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}

***

## Debugging

<figure><img src="../../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

There are 3 section displayed when the program is ran and debugged:

* **Registers:** Displays the current values of the registers after each instruction execution.
* **Code:** Displays where the executed instructions in the program flow are located.
* **Stack:** Displays where the elements in the stack data structure are located.

***

## Plugins

### PEDA (Python Exploit Development Assistance)

The PEDA (Python Exploit Development Assistance) plugin provides a more colorful and understandable interface to the user during debugging. The PEDA plugin can be downloaded from: [https://github.com/longld/peda](https://github.com/longld/peda).

#### Installation:

{% stepper %}
{% step %}
{% code overflow="wrap" %}
```bash
git clone https://github.com/longld/peda.git ~/peda
```
{% endcode %}
{% endstep %}

{% step %}
{% code overflow="wrap" %}
```bash
echo "source ~/peda/peda.py" >> ~/.gdbinit
```
{% endcode %}
{% endstep %}
{% endstepper %}
