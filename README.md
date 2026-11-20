**Networkwalks Academy | Cybersecurity & Ethical Hacking | Project Modules 1 & 2**

## Overview

This project explores password recovery from intentionally protected PDF files in an authorized training environment. I completed two workflows: using **John the Ripper with the Johnny graphical interface** and using the **Networkwalks browser-based Hash Calculator and Password Cracker**.

The exercises demonstrate how password-protected PDFs can be tested using extracted password-verification data and dictionary-based guessing. The results reinforce the importance of choosing strong, unique passwords.

## Objectives

- Extract a crackable representation of a password-protected PDF.
- Recover a test PDF password with John the Ripper / Johnny GUI.
- Perform a second password-recovery workflow with Networkwalks web tools.
- Verify the results by opening the protected training PDFs.
- Document evidence and defensive lessons learned.

## Tools

| Tool | Purpose |
| --- | --- |
| John the Ripper | Password recovery engine |
| Johnny GUI | Graphical interface for John the Ripper |
| OnlineHashCrack PDF Hash Extractor | Extract PDF password-verification data for Module 1 |
| Networkwalks Hash Calculator | Extract PDF hash data for Module 2 |
| Networkwalks Password Cracker | Test candidate passwords against the PDF hash |
| Adobe Acrobat | Verify that recovered passwords open the files |
| Windows / Web browser | Lab environment |

## Module 1 — John the Ripper and Johnny GUI

1. Obtained the password-protected PDF provided for the training lab.
2. Used the OnlineHashCrack PDF hash extractor to produce a John-compatible `$pdf$...` hash representation.
3. Loaded the extracted hash into Johnny GUI, configured to use the John the Ripper executable.
4. Ran a password-recovery attack and reviewed the recovered result.
5. Opened the PDF to validate access.

**Observed result:** Johnny displayed a recovered password of `good-luck` in my screenshot. The unlocked PDF displayed a congratulatory training flag. This result differs from the example password shown in the module's instructional guide, so the evidence below records my observed output rather than assuming the guide's result.

### Evidence

**PDF hash extraction**

<img width="960" height="564" alt="pdf1 hash" src="https://github.com/user-attachments/assets/76a47a40-0dd6-4e06-b530-cc2597ecaf67" />


**Recovered password in Johnny GUI**

<img width="496" height="392" alt="johnny password crack" src="https://github.com/user-attachments/assets/8e8d368b-1e48-44b2-a4be-26fcdcdd0163" />


**Opened PDF after password recovery**

<img width="960" height="564" alt="pdf1 cracked" src="https://github.com/user-attachments/assets/80108b8f-d224-4f38-b490-801731231fc0" />


## Module 2 — Networkwalks Hash Calculator and Password Cracker

1. Opened the Networkwalks Hash Calculator and selected the PDF extraction tab.
2. Loaded the password-protected training PDF and copied its `$pdf$...` hash representation.
3. Opened the Networkwalks Password Cracker and supplied the extracted hash.
4. Ran the tool's built-in dictionary attack and reviewed the result.
5. Opened the PDF to verify successful password recovery.

**Observed result:** The Networkwalks tool recovered `password1`. The screenshot shows a match after 91 of 100 candidates were tried. The PDF opened successfully and displayed the training flag.

### Evidence

**Networkwalks PDF hash extraction**

<img width="960" height="564" alt="networkwalks hash calculator" src="https://github.com/user-attachments/assets/dbc205b6-7485-4149-949a-211a1d2b9e28" />


**Successful dictionary attack**

<img width="960" height="564" alt="password cracker" src="https://github.com/user-attachments/assets/dc0d9ee9-509b-45f4-8983-92fc697d0018" />


**Opened PDF after recovery**

<img width="960" height="564" alt="pdf1 password cracked nw" src="https://github.com/user-attachments/assets/5783d370-136b-4b12-8e58-8c01fcc35ac2" />


## Technical Explanation

The `$pdf$...` string contains information used to test password guesses against the encrypted PDF. It is not simply a plaintext password or an ordinary hash of the document's contents. The cracking tool tests candidate passwords until it finds one that satisfies the PDF's password-verification mechanism.

A **dictionary attack** tries passwords from a predefined list. This approach is effective when a password is common or appears in the list, but failure to find a match does not prove a password is secure.

## Findings and Security Implications

| Finding | Evidence | Security implication |
| --- | --- | --- |
| A training PDF password was recovered with Johnny | Recovered `good-luck` | Guessable passwords can undermine file confidentiality |
| The Networkwalks dictionary attack succeeded | `password1` found within 100 candidates | Common passwords are vulnerable to small wordlists |
| Recovered credentials opened the protected PDFs | Both PDFs displayed their flags | Successful password recovery can provide access to protected contents |
| PDF password-verification data was extractable | `$pdf$...` output from both extraction workflows | Offline guessing may be possible without repeated interaction with the document owner |

## Defensive Recommendations

- Use long, unique, randomly generated passwords or passphrases for sensitive documents.
- Avoid common passwords, predictable patterns, and reused credentials.
- Use a trusted password manager to generate and store strong passwords.
- Protect sensitive documents with appropriate access controls and secure sharing practices; PDF passwords alone should not be the only security measure.
- Avoid uploading confidential files to third-party hash extraction services without authorization and an appropriate privacy review.

## Key Takeaways

This lab helped me understand the distinction between extracting password-verification data and recovering a password through guessing. I practiced both a desktop-based and a browser-based workflow, verified the results against the protected PDFs, and connected the exercise to real-world password security risks.

## Scope and Ethics

All testing was performed as part of an authorized Networkwalks Academy training exercise using designated lab PDFs. No third-party accounts or unauthorized systems were targeted.

