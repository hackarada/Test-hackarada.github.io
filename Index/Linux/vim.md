# vim

---

### **Undo changes in vim / Vi**

[https://www.cyberciti.biz/faq/vim-undo/](https://www.cyberciti.biz/faq/vim-undo/)

1. Press the Esc key to go back to the normal mode

        ESC

2. Type  to undo the last change.

        u

3. To undo the two last changes, you would type .

        2u

4. Press  to redo changes which were undone. In other words, undo the undos. Typically, known as redo.

        Ctrl-r

    other options

        :undo
        :undo N
        :undo 3
        
        ------
        :earlier {count}	Go to older text state {count} times.
        :earlier {N}s		Go to older text state about {N} seconds before.
        :earlier {N}m		Go to older text state about {N} minutes before.
        :earlier {N}h		Go to older text state about {N} hours before.
        :earlier {N}d		Go to older text state about {N} days before.
        :later {count}		Go to newer text state {count} times.
        :later {N}s		Go to newer text state about {N} seconds later.
        :later {N}m		Go to newer text state about {N} minutes later.
        :later {N}h		Go to newer text state about {N} hours later.
        :later {N}d		Go to newer text state about {N} days later.
        g-			Go to older text state.  With a count repeat that many times. 
        g+			Go to newer text state.  With a count repeat that many times.