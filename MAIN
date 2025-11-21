import sys
import argparse
import tkinter as tk
from tkinter import ttk, filedialog, messagebox


def shift_char(c, shift):
    if c.isalpha():
        base = ord('A') if c.isupper() else ord('a')
        return chr((ord(c) - base + shift) % 26 + base)
    return c


def caesar(text, shift):
    s = shift % 26
    return ''.join(shift_char(ch, s) for ch in text)


def encrypt(text, shift):
    return caesar(text, shift)


def decrypt(text, shift):
    return caesar(text, -shift)


def run_cli(args):
    if args.mode == 'encrypt':
        out = encrypt(args.text, args.shift)
    else:
        out = decrypt(args.text, args.shift)
    print(out)


class App:
    def __init__(self, root):
        self.root = root
        self.root.title('Caesar Cipher')
        try:
            style = ttk.Style()
            style.theme_use('vista')
        except Exception:
            pass
        main = ttk.Frame(root, padding=12)
        main.grid(row=0, column=0, sticky='nsew')
        root.columnconfigure(0, weight=1)
        root.rowconfigure(0, weight=1)

        lbl_msg = ttk.Label(main, text='Message')
        lbl_msg.grid(row=0, column=0, sticky='w')
        self.txt_in = tk.Text(main, height=6, wrap='word')
        self.txt_in.grid(row=1, column=0, columnspan=4, sticky='nsew', pady=(4, 8))

        lbl_shift = ttk.Label(main, text='Shift')
        lbl_shift.grid(row=2, column=0, sticky='w')
        self.shift_var = tk.IntVar(value=3)
        self.spn_shift = tk.Spinbox(main, from_=-25, to=25, textvariable=self.shift_var, width=6)
        self.spn_shift.grid(row=2, column=1, sticky='w')

        self.mode_var = tk.StringVar(value='encrypt')
        r1 = ttk.Radiobutton(main, text='Encrypt', variable=self.mode_var, value='encrypt')
        r2 = ttk.Radiobutton(main, text='Decrypt', variable=self.mode_var, value='decrypt')
        r1.grid(row=2, column=2, sticky='w')
        r2.grid(row=2, column=3, sticky='w')

        btn_run = ttk.Button(main, text='Run', command=self.on_run)
        btn_clear = ttk.Button(main, text='Clear', command=self.on_clear)
        btn_run.grid(row=3, column=0, sticky='w', pady=(8, 4))
        btn_clear.grid(row=3, column=1, sticky='w', pady=(8, 4))

        lbl_out = ttk.Label(main, text='Output')
        lbl_out.grid(row=4, column=0, sticky='w')
        self.txt_out = tk.Text(main, height=6, wrap='word', state='disabled')
        self.txt_out.grid(row=5, column=0, columnspan=4, sticky='nsew', pady=(4, 8))

        btn_copy = ttk.Button(main, text='Copy Output', command=self.on_copy)
        btn_save = ttk.Button(main, text='Save Output', command=self.on_save)
        btn_copy.grid(row=6, column=0, sticky='w')
        btn_save.grid(row=6, column=1, sticky='w')

        self.status = ttk.Label(main, text='', foreground='green')
        self.status.grid(row=7, column=0, columnspan=4, sticky='w', pady=(8, 0))

        main.columnconfigure(0, weight=1)
        main.columnconfigure(1, weight=0)
        main.columnconfigure(2, weight=0)
        main.columnconfigure(3, weight=0)
        main.rowconfigure(1, weight=1)
        main.rowconfigure(5, weight=1)

    def on_run(self):
        text = self.txt_in.get('1.0', 'end-1c')
        try:
            shift = int(self.shift_var.get())
        except Exception:
            messagebox.showerror('Error', 'Shift must be an integer')
            return
        mode = self.mode_var.get()
        if mode == 'encrypt':
            out = encrypt(text, shift)
        else:
            out = decrypt(text, shift)
        self.txt_out.configure(state='normal')
        self.txt_out.delete('1.0', 'end')
        self.txt_out.insert('1.0', out)
        self.txt_out.configure(state='disabled')
        self.status.config(text='Done')

    def on_clear(self):
        self.txt_in.delete('1.0', 'end')
        self.txt_out.configure(state='normal')
        self.txt_out.delete('1.0', 'end')
        self.txt_out.configure(state='disabled')
        self.status.config(text='')

    def on_copy(self):
        s = self.txt_out.get('1.0', 'end-1c')
        if not s:
            return
        self.root.clipboard_clear()
        self.root.clipboard_append(s)
        self.status.config(text='Copied to clipboard')

    def on_save(self):
        s = self.txt_out.get('1.0', 'end-1c')
        if not s:
            return
        path = filedialog.asksaveasfilename(defaultextension='.txt', filetypes=[('Text files', '*.txt'), ('All files', '*.*')])
        if not path:
            return
        try:
            with open(path, 'w', encoding='utf-8') as f:
                f.write(s)
            self.status.config(text='Saved')
        except Exception as e:
            messagebox.showerror('Error', str(e))


def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--text', type=str, help='Text to process')
    parser.add_argument('--shift', type=int, default=3)
    parser.add_argument('--mode', choices=['encrypt', 'decrypt'], default='encrypt')
    parser.add_argument('--cli', action='store_true')
    args = parser.parse_args()
    if args.cli or args.text is not None:
        if args.text is None:
            print('Missing --text')
            sys.exit(1)
        run_cli(args)
        return
    root = tk.Tk()
    App(root)
    root.mainloop()


if __name__ == '__main__':
    main()
