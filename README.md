import tweepy

# Chaves de acesso à API do Twitter
consumer_key = "SUA_CONSUMER_KEY"
consumer_secret = "SUA_CONSUMER_SECRET"
access_token = "SEU_ACCESS_TOKEN"
access_token_secret = "SEU_ACCESS_TOKEN_SECRET"

# Autenticar na API do Twitter
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

# Criar uma instância da API do Twitter
api = tweepy.API(auth)

# Pedir o nome de usuário do qual queremos obter os seguidores
username = input("Digite o nome de usuário do qual deseja obter os seguidores: ")

# Obter a lista de seguidores do usuário
followers = []
for follower in tweepy.Cursor(api.followers, screen_name=username).items():
    followers.append(follower)

# Imprimir o número total de seguidores
print("Número de seguidores: " + str(len(followers)))

# Para cada seguidor, obter as informações de perfil do Twitter
for follower in followers:
    user = api.get_user(follower.id_str)
    print("Nome de usuário: " + user.screen_name)
    print("Nome completo: " + user.name)
    print("Descrição do perfil: " + user.description)
    print("Localização: " + user.location)
    print("Número de seguidores: " + str(user.followers_count))
    print("Número de amigos: " + str(user.friends_count))
    print("Número de tweets: " + str(user.statuses_count))
    print("Data de criação da conta: " + str(user.created_at))
    print("URL do perfil: " + user.url)
    print("")
