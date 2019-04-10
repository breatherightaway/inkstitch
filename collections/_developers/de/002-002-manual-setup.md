---
title: "Manualle Installation"
permalink: /de/developers/inkstitch/manual-setup/
last_modified_at: 2019-04-10
toc: false
---
Eine manuelle Installation ermöglicht es am Quellcode zu arbeiten, während du Ink/Stitch benutzt.

1. Klone die Erweiterung und aktualisiere das Submodul pyembroidery

   ```
   git clone https://github.com/inkstitch/inkstitch
   cd inkstitch
   git submodule init
   git submodule update
   ```
2. Python Abhängigkeiten

    Es werden ein paar Python Module gebraucht. In einigen Fällen benutzt Ink/Stitch Funktionen, die nicht automatisch durch die Distributionen mit Python mitgeliefert werden.
    Deshalb empfehlen wir sie mit pip zu installieren:
    ```
    pip install -r requirements.txt
    ```

    **Info:** Evtl. musst du auf einigen Plattformen wxPython entfernen und ein platform-spezifisches Paket [installieren](https://wiki.wxpython.org/How%20to%20install%20wxPython):<br />
       ⚫ Debian `python-wxgtk3.0`<br />
       ⚫ Ubuntu 16.04: `pip install -U -f https://extras.wxpython.org/wxPython4/extras/linux/gtk3/ubuntu-16.04 wxPython`
    {: .notice--info }
    
    **Info:** Wenn du mehrere Python-Versionen installiert hast, nutze **pip2**
    {: .notice--info }

3. INX-Dateien vorbereiten

    ```
    for po in translations/*.po; do lang=${po%.*}; lang=${lang#*_}; mkdir -p locales/$lang/LC_MESSAGES; msgfmt $po -o locales/$lang/LC_MESSAGES/inkstitch.mo; done;
    mkdir inx
    bin/generate-inx-files
    ```

4. Symbolische Links in den Inkscape extensions-Order setzen

    ```
    cd ~/.config/inkscape/extensions
    ln -s /path/to/inkstitch
    for i in inkstitch/inx/inkstitch_*.inx; do ln -s $i; done
    ln -s inkstitch/inkstitch.py
    ```

5. Inkscape starten

**Info:** Änderungen am Python-Code werden wirksam, sobald die Erweiterung das nächste Mal gestartet wird. Änderungen an den INX-Dateien zeigen sich erst, nachdem Inkscape neu gestartet wurde.
{: .notice--info }