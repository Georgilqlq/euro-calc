<script>
    const currencies = [
		{
			id: 1,
			text: 'лв.'
		},
		{
			id: 2,
			text: '€'
		}
	];
    const rate = 1.95583;

    let selectedCurrency = $state();
    let given = $state();
    let cost = $state();

    let diffEuro = $derived.by(() => {
        if(selectedCurrency == currencies[0]){
            return (given / rate - cost).toFixed(2); 
        }

        return given - cost;
    });
    let diffLeva = $derived.by(() => {
        if(selectedCurrency == currencies[0]){
            return (given - cost * rate).toFixed(2);
        }

        return ((given - cost) * rate).toFixed(2);
    })
</script>

<div class="container content">    
    <div class="mb-3">
        <label for="cost" class="">Получена сума</label>
        <div class="input-group mb-3">
            <input id="cost" type="number" bind:value={given} class="form-control" aria-label="Text input with dropdown button">
            <select id="currency" class="form-select" bind:value={selectedCurrency}>
                {#each currencies as currency }
                    <option value={currency}>{currency.text}</option>
                {/each}
            </select>
        </div>
    </div>
    <div class="mb-3">
        <label for="total" class="">Дължима сума</label>
        <div class="input-group mb-3">
            <input id="total" type="number" bind:value={cost} class="form-control" aria-label="Text input with dropdown button">
            <span class="input-group-text">{currencies[1].text}</span>
        </div>
    </div>
    <div class="row">
        <div class="col-6">
            <label for="diffLeva" class="">Ресто в лева</label>
            <div class="input-group mb-3">
                <input id="diffLeva" value={diffLeva} type="number" readonly disabled class="form-control" aria-label="Text input with dropdown button">
                <span class="input-group-text">{currencies[0].text}</span>
            </div>
        </div>
        <div class="col-6">
            <label for="diffEuro" class="">Ресто в евро</label>
            <div class="input-group mb-3">
                <input id="diffEuro" value={diffEuro} type="number" readonly disabled class="form-control" aria-label="Text input with dropdown button">
                <span class="input-group-text">{currencies[1].text}</span>
            </div>
        </div>
    </div>
</div>
    
<style>
    .content{
        border: 1px solid var(--bs-border-color);
        border-radius: var(--bs-border-radius);
    }
</style>