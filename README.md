# ConvertSigmaRepo2KQL
A small crappy script I wrote that converts the Sigma Windows Process Creation events to KQL via PySigma. Designed for usage in unattended CI/CD scenarios, so you'll want to modify the directories used in the script to reflect your own scenarios.

All credit goes to the PySigma project: https://github.com/SigmaHQ/pySigma and the Defender backend, maintained by AttackIq: https://github.com/AttackIQ/pySigma-backend-microsoft365defender.

![image](https://github.com/rcegan/ConvertSigmaRepo2KQL/assets/5835816/e5677453-ac8b-4343-8e65-8908ac199b0d)

# Usage
Firstly, modify the 'rules_directory' variable to reflect the location of your Sigma process creation rules. If using in CI/CD and you're cloning the Sigma repo in each time, you can leave this value as-is.

Next, modify the 'output_directory' to match whichever folder you want the rules to be dumped into. Expect over 1000+ results.
