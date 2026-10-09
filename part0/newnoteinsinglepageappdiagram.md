```
sequenceDiagram
    participant browser
    participant server
    autonumber

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: 200 OK spa.html
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: 200 OK main.css
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: 200 OK spa.js
    deactivate server
	
	Note over browser, server: This (spa.js) is where the main difference is.

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: 200 OK data.json [{ "content": "hello world", "date": "2026-10-9" }, ... ]
    deactivate server

    Note over browser: User submits new note
    Note over browser: In spa.js, the input forms "onsubmit" function activates due to an event call. 
    Note over browser: The function pushes a note to the notes section and rerenders the list.
    Note over browser: Only then does the note get simply pushed to the server, no re-requests needed.

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa [{ "content": "67", "date": "2026-10-9" }]
    activate server
    server-->>browser: 201 Created 'message: "note created"'
    deactivate server
```