# Laravel

1. Installation:
    - Composer 
    - Docker => Sail
    - Herd

2. Folder Structure: (ruff idea)
    - composer.json
    - app
        - http
        - req (req from client)
        - res (res to client)
        - events/listeners
            - queue (for sending confirmation mails to users)
    - config
    - routes
    - storage
    - public 
        - assests
            - css
            - js
            - etc...

### definations and processes

1. spawn: if some process gonna fail in between and that's what called is spawn
2. syer visor - ( storing log files like and etc..) , comand
3. when spawn occurs so syer visor start the process again