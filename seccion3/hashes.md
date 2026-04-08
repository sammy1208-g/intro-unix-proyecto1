cat > seccion3/hashes.md << 'EOF'
# Sectio 3 - Hashes and Hashcat

## Comparative Hash Table

|| Password    || Length ||             Character Set                  || Approximate Entropy ||   Attack Method    ||             Cracking Time            ||  Results   ||
||-------------||--------||--------------------------------------------||---------------------||--------------------||--------------------------------------||------------||
||12345678     ||   8    || Only numbers (0-9)                         ||    ≈26 bits         || Dictionary Attack  ||  A Few Seconds (4s)                 ||  Cracked    ||
||-------------||--------||--------------------------------------------||---------------------||--------------------||--------------------------------------||------------||
||C0ntr4M3d#$  ||  10    || Uppercase, Lowercase, Numbers, and Symbols ||    ≈65 bits         || Brute Force        || >30 minutes (on a VM without a GPU) || Not cracked ||

EOF
