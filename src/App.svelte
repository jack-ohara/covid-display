<script>
  const fetchData = (async () => {
    const response = await fetch('https://api.coronavirus.data.gov.uk/v1/data?filters=areaType=nation;areaName=england&structure={"date":"date","newCases":"newCasesByPublishDate", "cumCases":"cumCasesByPublishDate"}');
    console.log(response);
    return await response.json();
  })();
</script>

{#await fetchData}
  <p>Loading...</p>
{:then data}
  <p>{JSON.stringify(data)}</p>
{:catch error}
  <p>Oops... {error}</p>
{/await}