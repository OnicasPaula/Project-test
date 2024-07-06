import openai

# Configurare API OpenAI
openai.api_key = 'your-api-key-here'

# Funcție pentru a genera oferta
def generate_offer(client_requirements):
    # Prompt pentru modelul de limbaj
    prompt = f"""
    Clientul a solicitat următoarele funcționalități pentru aplicația sa:
    {client_requirements}

    Pe baza acestor cerințe, te rog să generezi o ofertă detaliată care să includă:
    - Descrierea aplicației solicitate.
    - Tehnologiile folosite pentru dezvoltarea aplicației (ex: stack tehnologic - front-end, back-end, baze de date, etc.).
    - Task-urile concrete și detaliate necesare pentru dezvoltarea aplicației, inclusiv cele care nu sunt menționate direct de client dar sunt necesare (ex: secțiuni financiare, facturare, etc.).

    Oferta:
    """

    # Solicitare către API-ul OpenAI
    response = openai.Completion.create(
        engine="text-davinci-003",
        prompt=prompt,
        max_tokens=1500,
        n=1,
        stop=None,
        temperature=0.7
    )

    # Extrage textul generat de AI
    offer = response.choices[0].text.strip()
    return offer

# Cerințele clientului
client_requirements = """
1. Sofer:
  - Harta cu traseul său care să conțină punctele de ridicare și livrare.
  - Timpul estimat pentru ambele.
  - Posibilitatea de a prelua singur o solicitare de la un restaurant sau să i se acorde livrări.
  - Raport zilnic cu livrările efectuate.
  - Actualizare în timp real al parcursului său către client.
2. Restaurant:
  - Preluare comenzi, confirmarea lor și a statusului comenzii în timp real către client.
  - În orele de vârf să nu mai aibă clientul opțiunea de a pune noi comenzi dacă durează mai mult decât timpul estimat în aplicație.
  - Solicitare șofer și opțiunea de a vedea parcursul șoferului.
3. Client:
  - Să ia la cunoștință toate detaliile legate de restaurant (timp estimat de livrare, timp de preparare etc).
  - Să adauge produse în coș, achiziție cu card sau numerar din aplicație.
  - Să primească notificări cu fiecare parcurs al comenzii (confirmată, comanda urmează să fie ridicată, comanda a fost ridicată, comanda livrată).
  - După plasarea și confirmarea și preluarea comenzii de către șofer să i se prezinte șoferul, numărul de contact al acestuia și parcursul său pe hartă.
4. Funcție Admin:
  - Monitorizare activitatea celor 3 ramuri menționate și posibilitatea de a efectua un raport pe fiecare.
  - Opțiune pentru livrări de colete mici sau plicuri, unde să se ofere câteva informații despre colet (dacă e plic sau e o cutie și ce dimensiuni/greutate are).
"""

# Generarea ofertei
offer = generate_offer(client_requirements)

# Afișează oferta generată
print(offer)
![image](https://github.com/OnicasPaula/Project-test/assets/105229346/de7dbb02-19b8-4b8e-a28f-f799fa3f9de1)
