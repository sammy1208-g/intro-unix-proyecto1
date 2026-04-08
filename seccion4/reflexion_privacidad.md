cat > seccion4/reflexion_privacidad.md << 'EOF'
# Sección 4 - Reflection on Privacy and Secure Email

## Reflection
 
During the development of this section, we learned that security in digital communications goes far beyond simply using a password. The use of GPG and ProtonMail allowed us to understand how asymmetric encryption works in practice: signing a message guarantees the sender's identity, while encrypting it ensures that only the recipient can read the content.
It was especially relevant to discover that even with active end-to-end encryption, email metadata (who is writing to whom, when, and from where) remains visible to intermediaries. This demonstrates that digital privacy requires multiple layers of protection, not just one.
The comparison between ProtonMail, Gmail, and Outlook showed that the provider's legal jurisdiction matters as much as its technical characteristics. Operating under Swiss privacy laws represents a real advantage over providers subject to US legislation such as the Cloud Act.
Finally, learning about Ecuador's LOPDP and the GDPR allowed us to recognize that citizens have specific rights over their digital data, including email, and that legal mechanisms exist to exercise and protect these rights.


## Question 1 - Asymmetric Encryption

Asymmetric encryption uses a key pair, and its operation in GPG is as follows:
• Public --> It is freely shared. It can be used to encrypt messages that only you can open, or to verify your signature.
• Private --> Secret. It is used to decrypt messages encrypted with our public key, or to sign.

Differences: 
• Encrypt  The sender uses the recipient's public key; only the recipient can decrypt it. This protects the content.
• Sign    The sender uses their private key; anyone can verify it with the public key. This verifies identity and authenticity.


## Question 2 - Comparativa ProtonMail vs Gmail vs Outlook

Feature	              ||       ProtonMail	                   ||        Gmail                          ||Outlook                                                     ||
----------------------||------------------------------------------ ||---------------------------------------||----------------------------------------------------------- ||
Encryption at rest    || Yes, it's encrypted with zero-knowledge.  ||Yes, but Google has access to the keys.|| Yes, Microsoft has access to the keys.                     ||
--------------------- ||-------------------------------------------||---------------------------------------||----------------------------------------------------------- ||
Encryption in transit ||TLS (SMTP/IMAP)	                           || Standard TLS	                    || Standard TLS                                               ||
----------------------||-------------------------------------------||---------------------------------------||----------------------------------------------------------- ||
End-to-end Encryption || Native between ProtonMail users, Open PGP || Not native, requires S/MIME extension.|| S/MIME in Enterprise plans, not native on Web.             ||
                      || with external users.                      ||                                       ||	                                                          ||
------------- --------||-------------------------------------------||---------------------------------------||----------------------------------------------------------- ||
Provider privacy and  || The content is inaccessible. Data is not  ||It can analyze data for advertising.   || Microsoft may be accessed for support and legal compliance.||
data access policies  || sold.                                     ||It complies with legal orders.	    ||                                                            ||   
----------------------||-------------------------------------------||---------------------------------------||------------------------------------------------------------||
Jurisdiction	      ||Switzerland. Very strict privacy laws,     || USA Subject to FISA, CLOUD Act.       || US Subject to CLOUD Act, also servers in EU.               ||  
                      || outside the EU/Five Eyes.	           ||                                       ||	                                                          ||


## Question 3 - PKI vs Web of Trust

--> PKI (Public Key Infrastructure) with CA: It is a trusted central authority that signs and validates keys/certificates.
--> Web of Trust (WoT): It's a decentralized GPG model, where users sign each other's keys, creating a transitive trust network. There is no central authority.

	       || PKI with CA	                                                                 ||                               Web of Trust
---------------||--------------------------------------------------------------------------------||----------------------------------------------------------------------------------------
Advantages     || • Automatic and scalable trust (works over HTTPS without user configuration).  || • Decentralized, since no single entity can compromise the entire system.
               || • Rapid and standardized (CRL/OSCP).	                                         || •	Censorship-resistant and resistant to single points of failure.
---------------||--------------------------------------------------------------------------------||----------------------------------------------------------------------------------------- 
Disadvantages  || • If a CA is compromised, it affects millions.                                 || • Requires users to manually manage trust (not very user-friendly for the general public).
               || • Centralized, since governments can pressure CAs to issue fake certificates.	 || • Difficult to scale; the trust network may have gaps or be weak for new users.


## Question 4 - GDPR vs LOPDP Ecuador

Feature	                  ||   GDPR (UE)                           ||   LOPDP (Ecuador)
--------------------------||---------------------------------------||--------------------------------------
Year of entry into force  ||   2018	                           ||       2021                          
--------------------------||---------------------------------------||------------------------------------ 
Application	          || Any organization that processes data  || Any natural or legal person who     
                          || of residents in the EU.	           || processes data of Ecuadorians.      
--------------------------||---------------------------------------||------------------------------------ 
Right of access	          ||Yes, citizens can request what data    || Yes, expressly recognized           
                          || the organization has.	           || (Art. 13 LOPDP, 15-day period).     
--------------------------||---------------------------------------||-----------------------------------  
Right to be forgotten/    || Yes, you have the right to have your  ||Yes, recognized as a right to 
erased                    || data erased (Art. 17 GDPR).	   || elimination.
--------------------------||---------------------------------------||---------------------------------
Right to portability	  || Yes, receive your data in a structured|| Yes.
                          || format.	                           ||
--------------------------||---------------------------------------||----------------------------------
Right to object	          ||Yes, to oppose the treatment.	   || Yes.
--------------------------||---------------------------------------||-----------------------------------
Consent	                  || Explicit, informed and revocable.	   || Free, prior, specific and informed.
--------------------------||--- -----------------------------------||-----------------------------------
Email	                  || Emails containing personal data are   || Even with protection, he has private
			  || protected data; the provider must     ||communications, these are inviolable
		          || guarantee their security.	           ||(Art. 66 CRE).
--------------------------||---------------------------------------||----------------------------------
Digital Surveillance	  || It prohibits mass surveillance without|| Protects against illegal interception;
                          || a legal basis and recognizes privacy  || surveillance requires a court order.
			  || as a fundamental right.	           ||
--------------------------||---------------------------------------||------------------------------------
Supervisory authority	  ||Each country has its own DPA.	   ||Superintendency of Personal Data Protection.
--------------------------||---------------------------------------||------------------------------------
Sanctions	          ||Up to €20 million or 4% of global turnover.|| Up to USD 20,000 or a percentage of income.


## Question 5 - Email Metadata

Metadata is information about the message, not the content itself. In an email, it includes:
•From/To/CC: It’s the sender and the recipient.
•Date/ Time: When it was sent.
•IP address of the source server.
•Subject
•Message-ID, References: Thread Identifiers.
•User-Agent: Email client used.
•Message size.

End-to-end encryption only protects the message body. Metadata must travel in plain text because the SMTP protocol needs it to route email, just as a postal envelope must show the address, even if the envelope is sealed. This means that any intermediary server can see who you are communicating with, when, and from where, without reading any of the message This has serious privacy implications. From metadata, it's possible to reconstruct entire communication networks, infer political, medical, or personal relationships, and build detailed behavioral profiles, all without having to decrypt the content.
EOF
