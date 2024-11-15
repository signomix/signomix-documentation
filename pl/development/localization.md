# Lokalizacja tekstów na stronach webaplikacji

Przygotowanie strony w różnych wersjach językowych i prezentowanie użytkownikowi wybranej wersji językowej.


Przykład pliku `+page.svelte` 
```
<!-- +page.svelte -->
<div>
    <h5>{utils.getLabel('about',labels,session)}</h5>
</div>
<div>
    {utils.getLabel('description',labels,session)}
</div>
<script>
    import { userSession } from '$lib/stores.js';
    import { utils } from '$lib/utils.js';
    
    let session;
    userSession.subscribe(value => {
        session = value;
    });

    let labels = {
        'about': {
            'pl': "O aplikacji",
            'en': "About"
        },
        'description': {
            'pl': "Opis aplikacji ...",
            'en': "Application description ..."
        }
    }
</script>
```