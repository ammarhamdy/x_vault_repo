
# Installation

```sh
git clone https://github.com/digininja/RSMangler.git
```

```sh
sudo ln -s /opt/RSMangler/rsmangler.rb /usr/local/bin/rsmangler
sudo chmod +x /opt/RSMangler/rsmangler.rb
```

# Eamples

```sh
rsmangler -f target.txt --min 12 --na >> mangler-wordlist.txt
```

```sh
rsmangler -f target.txt --min 12 --years >> mangler-wordlist.txt
```

```sh
rsmangler -f target.txt --min 12 --nb >> mangler-wordlist.txt
```