cat > seccion2/calculo_entropia.md << 'EOF'
# Section 2 - Entropy Calculation
## Manual Calculations
1. 
Formula: H = L × log₂(N) 
Where: H = Entropy in bits
L = Password length (number of characters) 
N = Alphabet size (total possible characters
Password 1: MyKeePass@2025!Secure
KeePassXC Assessment:)
Password: MyKeePass@2025!Secure
Characters: 21
Entropy (KeePassXC): 53.14 bits
Quality Rating: Débil (Weak)
Analysis: Even though 21 characters long, used uppercase, lowercase letters, numbers, and special characters (i.e. @ and !), and would be considered strong, KeePassXC indicates that this is weak because of only 53.14 bits of entropy.

2. 
Password 2: n4rFQN23VY^fS7gE#fj
KeePassXC Assessment:
Password: n4rFQN23VY^fS7gE#fj
Characters: 19
Entropy (KeePassXC): 109.24 bits 
Quality Rating: Excelente (Excellent)
KeePassXC has determined that this password scores EXCELLENT based on its entropy of 109.24 bits and length of 19 characters. The reason this password is superior to Password 1, which has a longer character count, can be attributed to several things including:
Complete randomization — contains no recognizable words, patterns, or recognizable sequences.

3. 
Password 3: Github@2024Dev
KeePassXC Assessment:
Password: Github@2024Dev
Characters: 14
Entropy (KeePassXC): 44.72 bits
Quality Rating: Débil (Weak)
Evaluation:
This password would receive a strong score of "WEAK" per KeePassXC and only contains 44.72 bits of entropy.
EOF
