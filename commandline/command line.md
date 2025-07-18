### VI editor 

vi ~/.zshrc
ps au 
ps aux
ps aux|grep 45934


shift +g takes to the bottom offile 
:q quit 
:q! ----> quit and dont save any changes
:/jenv ---> search 
:1 ------> takes me to first line 
:d10-----> deletes 10 lines 
u ----> undo 



less --->displays the content inside the document 
cat ----> prints the content of document on the console
tail ---> anything that is getting added to the file will be printed 

java -Xms -Xmx
-->to set minimum and maximum heap size 


nano editor shortcuts 




Love the hands-on spirit! Let’s make this a little Linux/Unix $PATH + Node/npm config exercise you won’t forget. 🔥

I’ll guide you step-by-step and then give you a quick summary at the end for your brain to lock it in.

---

## **💡 Goal:**

  

Make sure /usr/local/bin is part of your $PATH so your system can find node and npm.

---

## **✅ Step-by-step:**

  

### **1.** 

### **Check if Node.js is working**

  

Run:

```
node -v
```

👉 If it shows v22.15.0, you’re golden.

If not, it means your system can’t find the node binary yet — time to fix that with $PATH.

---

### **2.** 

### **Check your current $PATH**

  

Run:

```
echo $PATH
```

Look for /usr/local/bin in the output. If it’s **already there**, you’re done! If not, proceed to next step.

---

### **3.** 

### **Add /usr/local/bin to your PATH (if needed)**

  

Depending on your shell (bash or zsh), you’ll add it to your shell config file.

  

### **🔎 First, find out your shell:**

```
echo $SHELL
```

- If it says /bin/zsh, open .zshrc
    
- If it says /bin/bash, open .bash_profile or .bashrc
    

  

### **🛠 Edit your file:**

```
nano ~/.zshrc   # or ~/.bash_profile or ~/.bashrc depending on above
```

### **✍️ Add this line at the bottom (only if it’s not already present):**

```
export PATH="/usr/local/bin:$PATH"
```

Then save and exit.

---

### **4.** 

### **Apply the changes**

  

After updating your config file, run:

```
source ~/.zshrc   # or source ~/.bash_profile
```

  

---

### **5.** 

### **Verify everything works**

  

Now again try:

```
node -v
npm -v
```

🎯 You should see:

- v22.15.0
    
- v10.9.2
    

---

## **🧠 TL;DR – LOCK THIS IN YOUR BRAIN:**

| **🧩 Task**        | **💻 Command**                            |
| ------------------ | ----------------------------------------- |
| Check Node version | node -v                                   |
| Check current PATH | echo $PATH                                |
| Edit shell config  | nano ~/.zshrc or nano ~/.bash_profile     |
| Add path line      | export PATH="/usr/local/bin:$PATH"        |
| Apply changes      | source ~/.zshrc or source ~/.bash_profile |
| Confirm setup      | node -v && npm -v                         |

  

---

Wanna try this and I’ll validate what you did? Let’s roll! 😎