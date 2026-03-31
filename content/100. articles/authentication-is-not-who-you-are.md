---
title: Authentication is not who you are
publish: false
draft: true
tags:
  - articles
  - IAM
---

Terminology in the Identity and Access Management (IAM) space is a mess. We have competing definitions, insufficiently precise terms, and multiple terms that refer to the same thing. Many terms are also used in a loose, colloquial form. For example, we might conflate “identity” and “person.” Someone might say “we saw Alice log in at 2:55PM”, as if they were standing over Alice’s shoulder watching her logging into the system. We talk about “authenticating the user” as if the system is actually reaching through the screen and verifying a human soul.

This loose use of terminology may have its place, but from an architectural standpoint, that’s a dangerous fiction. Systems don’t know people; they know only records in a database. When we forget that authentication is merely a proxy—a successful proof of control over an authenticator, not proof of who is at the keyboard—we leave the door open for security debt that no amount of MFA can fully repay.

The Cost of Colloquialism

The terminology in the Identity and Access Management (IAM) space is notoriously messy. We deal with overlapping terms, competing vendor definitions, and—most commonly—the colloquial use of technical language that muddies the water for everyone involved.

While “proving who you are” is a convenient shorthand for a non-specialist, it creates a fog that even experts struggle to navigate. We see this play out most clearly on support calls: a Help Desk technician asks to “verify an identity,” while the user on the other end is frustrated because they know who they are—they just can’t get the system to “recognize” them.

The technician is looking for a match between a claim and a database record; the user is looking for a human acknowledgement. When we use IAM terms colloquially, we don’t just confuse our architectures—we confuse our people.

Context: the typical “user logging in” scenario, which most often looks like the presentation of an identifier and an authenticator, which in turn most often looks like a username or email address, and a password.



Authentication is proving you are who you claim to be.

This is a common refrain. It is wrong.

When you log into a system, the system does not know who you are. The system has only a database of information about registered users. When you log in, you present an identifier, and some sort of authenticator. The identifier you provide is a key into a database. When you present your identifier, you are making a claim, not about who you are but that you are entitled to exercise the privileges assigned to the digital persona associated with the identifier you provided. You prove that you are entitled to this by providing the authenticators bound to the identity. We take on the assumption that whoever controls the required authenticators, is the legitimate user.

The identifier you provide the system does not identify you. It identifies a digital identity in a database, and it functions as a claim. You are claiming to be this person associated with the identity. You are saying “I am in control of the authenticators associated with this digital identity, and I am therefore entitled to exercise the privileges associated with that digital identity.

What is an identifier?

Most commonly a username (self-selected or assigned) or an email address, the identifier is how you tell the system who you are claiming to be.

III. The Authenticator: Proof of Control

**NIST’s Rigor:** Define authenticators as something the claimant **possesses and controls**. 

**The Proxy Problem:** Success in authentication only proves that the required “math” (cryptographic module) or “memory” (password) was presented. 

**Modern Examples:** Briefly touch on why a FIDO2 credential or a passkey is the modern gold standard of this “proof of control.” 

NIST defines an authenticator as … (I don’t like constructs like “ABC defines FOO as …” Appeal to authority?

What is an authenticator?

Most commonly a password (shared secret), NIST provides a broader definition:



Something the claimant possesses and controls (typically a cryptographic module or password) that is used to authenticate the claimant’s identity. — NIST SP 800-63-3

Particularly relevant today, a FIDO credential, including a passkey, is an authenticator. Passkeys are particularly valuable as they blah blah blah…

IV. The Principal Insight: The Security Gap

**The Risk:** Anyone—an attacker, a bot, or a malicious insider—who gains control of the authenticator *is* the user for all intents and purposes. 

**The Consequences:** Why “Authentication” is a weak proxy for “Identity” without secondary layers like **Identity Assurance** and **Risk Analysis**. 

**The Architectural Shift:** Stop designing systems that trust the *person* because they passed AuthN; start designing systems that trust the *authenticator* based on its strength.

Anyone, including, importantly, an attacker, with control of the authenticators for an identity can exercise the privileges of that identity.

### V. Conclusion

Authentication demonstrates control of the keys to a digital identity.

**The Takeaway:** If you don’t understand that AuthN is just a proxy, you will always over-estimate your system’s security.

Why does this matter?

If you need to know that the person logging in is who you expect to be logging in, you need to:





Perform some form of strong identity verification when the subject first registers, and



Bind sufficiently strong authenticators to that identity as part of the registration flow.

You cannot wait until some time later to attach strong authenticators to the identity. If you want to attach stronger authenticators to the identity some time after the identity has been established, you need to repeat your identity verification exercise. You need to be confident the person at the keyboard adding