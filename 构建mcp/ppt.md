# client
expose roots,sampling
# server:
exposes tools resources,prompt Tempalets

optanl feature in model context protocol

std transport can use environments variables

remote servers need something different

# roots

a root is a URI that a client suggest a server should operate

only look in these specific folders for the files I need.

when a client connects to a server,it declares which root the server should work with.

while primarily used for filesystem paths,roots can be any valid UI including HTTP URLs

beneifies:

suecirty:limits server access to hust the specified directories or endpoints

clarity:keeps the server focused on the releveant resources/locations

versatitly while often used for files,root can be any valid URI.

# mcp clients

invoke tools,queries for resources,interpolates prompts

mcp servers:exposes tools,exposes resources,exposes prompt templates

<img width="961" height="536" alt="image" src="https://github.com/user-attachments/assets/d33849e5-ccde-41a1-af64-7c2dd77bc95b" />


# resources

allow the mcp server to expose data to the client

similart to get requets handlers in a typical http server

can return any type of adatas strings,JSON,binary,etc

you set the mine_type to give the client a hint as to what data you are returning

two types:direct and templated

# defining a tool

mcp provides sdk's for building servers and clients in a variety of languages

you will be using the python mcp sdk

the python sdk make it very easy to declare tools

the service provider itself will makr their own mcp implementation you can make a mcp server to wrap up access to some service

mcp server provide tool schemas +functions

if you want to directly call an api directly,you ll be authoring those on your own.

mcp servers provide tool schemas +funcions already defined for you.


