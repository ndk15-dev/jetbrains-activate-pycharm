In some cases, only these lines will work
```sh
for product in IntelliJIdea WebStorm DataGrip PhpStorm CLion PyCharm GoLand RubyMine; do
    rm -rf ~/.config/$product*/eval 2> /dev/null
    rm -rf ~/.config/JetBrains/$product*/eval 2> /dev/null
done
```

But if not, try these

```sh
#!/bin/bash

# List of JetBrains IDE products
for product in IntelliJIdea WebStorm DataGrip PhpStorm CLion PyCharm GoLand RubyMine; do
    echo "[+] Resetting trial period for $product"

    # Remove evaluation key directories (older paths)
    echo "[+] Removing Evaluation Key (old path)..."
    rm -rf ~/.config/"$product"*/eval 2> /dev/null

    # Remove evaluation key directories (newer paths)
    echo "[+] Removing Evaluation Key (new path)..."
    rm -rf ~/.config/JetBrains/"$product"*/eval 2> /dev/null

    # Remove 'evlsprt' properties from options XML file (older paths)
    echo "[+] Removing all 'evlsprt' properties in options.xml (old path)..."
    sed -i 's/evlsprt//' ~/.config/"$product"*/options/other.xml 2> /dev/null

    # Remove 'evlsprt' properties from options XML file (newer paths)
    echo "[+] Removing all 'evlsprt' properties in options.xml (new path)..."
    sed -i 's/evlsprt//' ~/.config/JetBrains/"$product"*/options/other.xml 2> /dev/null

    echo # Newline for readability
done

# Remove Java user preferences directory
echo "Removing userPrefs files..."
rm -rf ~/.java/.userPrefs 2> /dev/null

echo "Reset complete."
```

If not works on Mac OS, then run the following code:
```sh
rm -rf ~/Library/Preferences/com.apple.java.util.prefs.plist
```
