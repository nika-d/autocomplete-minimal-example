<script>
    import AutoComplete from 'simple-svelte-autocomplete'
    import {tick} from 'svelte'

    let selectedItem
    let items = [
        {label: 'circle'},
        {label: 'rectangle'},
        {label: 'triangle'}
    ]

    async function select(item){
        await tick()
        selectedItem = item
    }

    function setValueAndOptions(){
        items = [
            {label: 'nandu'},
            {label: 'lynx'},
            {label: 'tapir'}
        ]
        select(items[0])
    }

</script>

<section style="width: 70%">
    <h3>Unexpected behavior of simple-svelte-autocomplete:</h3>
    <p>Let´s say, the autocomplete was already rendered once, with some list of possible choices in <code>items</code>.
        Everything fine so far. Now, when we change the <code>selectedItem</code> and the <code>items</code>, and then
        click into the autocomplete field, we see: autocomplete still uses the old value of the options!
    </p>
    <p>Reproduce: </p>
    <ol>
        <li>Hit the button:
            <button on:click={setValueAndOptions}>
                Set options to animals and value to nandu
            </button>
        </li>
        <li>Click into the autocomplete field.Autocomplete options open, but you see the old options.</li>
    </ol>
    <AutoComplete debug labelFieldName="label" bind:selectedItem={selectedItem}  items={items}/>
    <p>Autocomplete options are: <br>
        {#each items as item}{item.label} {/each}</p>
    <p>For a reset please reload the page.</p>
    <h3> Second unexpected behavior:</h3>
    <p>Event handler seem not to be called. Checked with beforeChange, onChange and onFocus. They are called once when the autocomplete is created, but then never again.</p>
</section>
