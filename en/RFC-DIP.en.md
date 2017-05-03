
# RFC Decidim Identity Protocol

## ToC

* [Summary](#DIP-summary)
* [Technical Specs](#DIP-specs)
* [Discussion](#discussion)


## <a name="DIP-summary"></a> Summary

DIP (Decidim Identity Protocol) is a system for registration, authentication and verification of digital identities promoted by the Decidim project. It is promoted both as a principle as well as an open infraestructure for digital identification and, by extension, as a system of access to concrete actions or the exercise of concrete rights. We can describe it as a system of anonymous digital identity that is administratively certified, privately guarded and publicly verifiable. 
The rest of this section explains in detail what it is and how it works. 

In synthesis: 1-the user registers in the system (a username associated to an e-mail account and a password), 2-authentication data are requested (this could be census data or a unique identifying number sent via post mail or picked up at a municipal office); 3-the user account is authenticated and no data are kept from the verification process. In this way the user can make use of a “digital body” and exercise a series of rights in the democratic digital space without anybody being able to connect its digital identity with its personal identity. This process guarantees that only an account exists for any given user with a given set of juridical and social rights, and that, at the same time, every individual can have an account. Otherwise, we ensure that the mapping between system users and individuals or persons is one-to-one while the system remains ignorant concerning who-is-who. 

But we can go beyond this: it could be the citizenry the actor guarding its authenticated digital identity, without depending on a centralized service, and to make it valid in relation to other agents without the mediation of the City Council. We could even make public agreements, verifiable by anyone, among citizens, without the mediation of the City Council and, moreover, with the same juridical validity as if the City Council was backing it up. And all of this without renouncing to privacy. Even if it sounds magic, existing technology allows to do this. 
All of this would be impossible without the Decidim Identity Protocol based in a combination of (warning: technical terms ahead) asymmetric cryptography and public-ledger, distributed systems. If you already know what these terms mean you can skip the next section and go directly to the technical description.

### <a name="DIP-specs"></a>Technical Specifications

Basically, DIP (Decidim Identity Protocol) is based in a decentralized anonimity system that uses authenticationo, is based in public-private certificates (or asymmetric cryptography) managed with distributed technology (blockchain or bit torrent type). The [Decidim](https://decidim.github.io) platform operates as a front end and mediation interface for a distributed system of storage and access to identities and contents, as well as decentralized intermediary of a centralized authentication service (f.i.: a city census). 

0. **User registration and authentication**: this is the system currently working in Decidim. People register with a user name, an e-mail and a password associated to decidim. In order to finish the registration they have to verify their email address. After the user is registered and has a verified email, she can move to be authenticated as a citizen of Barcelona. For that, additional personal data (full name, birth date, postal address) are requested in order to autheticate the identity and a query is made to the city census in order to  validate them. The user could also be authenticated with a personal code sent to the user’s address, or a sms. After the data have been checked, the digital identity is marked as authenticated, but no data from the authentication process are stored (except for those strictly necessary for revoking that identity, f.i.: an ID hash is kept [^1]).
![Registration and user verification](https://i.imgur.com/7E5YWen.png)



1. **Generation and storage of private keys**: an objective is to make the private key generation process reproducible. On top of a password for de-crypting the private key (in its usual storage space) it would be good to have a private key generator combining a password (it could be the one use for the encryption) with private data that only the owner of the key knows but also allows the entry entropy and thereby the security of the process. This type of system is common in the generation of bitcoin wallets. The key can be safely stored in the user’s mobile or other devices (f.i.: in a USB key) or a computer folder (for users that do not want or cannot rely on a mobile and have the necessary competences). The Mobile ID system promoted by the Barcelona City Council could be used to generate and store the key in an easy way for non-experts. This is a great advantage because the problem with asymmetric encryption systems is, precisely, the access barriers in the management and security of those keys. Mobile ID is an ideal platform to break this barrier because it is an easy to install and easy to use app. 
![Generation and storage of private keys](https://i.imgur.com/lonhiGi.png)

2. **Public key verification**: when a verified user signs into Decidim she can choose to verify her publlic key. For that she can upload her public key (this operation can be carried on via mobile or via pc). The public key is signed with the city council’s private key, it is re-sent to the user and published in an official Decidim list where it is shared on a blockchain system. The client should  make a push to other servers to guarantee that her signed public key is really published.  

![Public key verification](https://i.imgur.com/O7fMB7d.png)

3. **Signatures, contracts, and public verification**: from then on, when a user gives support to a political initiative or proposal she signs it with her private key and the signed initiative is published. This publication is distributed afterwards, or may even be signed in a distributed manner. Even Decidim allows to do this taking advantage of the usability, quality of service and recourse to a centralized service, such centralization is not required for the functioning of the system.

![Signatures, contracts, and public verification](https://i.imgur.com/hUMWd2H.png)


## <a name="discussion"></a>Discussion 

The central problem of the DIP is the revoking in case of corruption, losses or theft of a user’s private ky, as well as the required measures to avoid double verifications. To solve this is not easy: either we go back to a (semi)centralized verification system or we lose anonymity. All solutions require to balance three factors: 1-decentralization, 2-univocal authentication, 3-anonimity. The different solutions result in different equilibria in which either anonimity warranties are sacrificed to ensure authentication or there is less decentralization in order to guarantee anonimity. 

One of the big problems for finding the best equilibrium is to attend to three very different types of identity uses in the exercise of democratic rights (these services require different equilibria between decentralization, anonimity and authentication): 

* Voting
* Signatures
* Assemblies

For voting privacy protection (or anonimity) is only important in order to prevent that a person is associated to her vote. In polling places names and census Ids are available and visible, and the individual´s identity is checked. This is not a problem if there are guarantees that the vote is secret. Otherwise, it does not matter if the identity of the person is revealed insofar as the vote is kept secret, if what she votes remains unknown. There exists digital cryptographic technologies that, separating the voting poll that identifies you (the server that manages the identities), from the ballot box  and the counting process (mixers and mathematical reconstruction of the results) can guarantee with enough guarantees the protection of the secrecy of the vote. 

But if the same digital identity system that requires to be used for the digital signature (a signature like the one required for a legislative initiative) and, moreover, we want that the counting of signatures remains auditable, we enter a different scenario, one in which anonymity is authentified anonimity is required to ensure ethe privacy of the signatures. 

Another problem found at Decidim lies in the fact that the platform is oriented to facilitate the integration between physical and virtual participation. In many cases it is necessary to register for an assembly (in order to predict the number of attendants) and we then enter another difficult connected to identities: how do I protect the privacy of a person that gets into a room where an assembly is running and that has signed up digitally, but two others appear saying the same and there is no room for everyone? 

We still have problems to solve. The decisions that we take on this will condition the exercise of democratic rights in the future. Nor Facebook, nor Google, nor Twitter have a genuine interes in democratizing society (or their interest is proportional to the democracy of their board of directors or their market value). There are initiatives  (f.i.  [Onename](https://onename.com/), [Sovrin](https://sovrin.org/) or the EU project [Decode](http://www.decodeproject.eu/)), but the lack the institutional anchoring, an operating interface and the pragmatics of participation platforms such as Decidim in order to attract and legitimate the use of these systems. The future is in our hands.

We are currently working with DECODE to develop this infrastructure together. Comments are welcome.



[^1]: There is still much room for improvement on Decidim's privacy on this matter.