<script lang="ts">
  const AreaType: string = "overview";
  const AreaName: string = "england";

  const filters = [
        `areaType=${ AreaType }`,
        //`areaName=${ AreaName }`
    ];
  const structure = {
      date: "date",
      //name: "areaName",
      code: "areaCode",
      cases: {
          daily: "newCasesByPublishDate",
          cumulative: "cumCasesByPublishDate"
      },
      deaths: {
          daily: "newDeathsByDeathDate",
          cumulative: "cumDeathsByDeathDate"
      }
  };

  const apiParams: string = `filters=${ filters.join(";") }&structure=${ JSON.stringify(structure) }`;
  const encodedParams: string = encodeURI(apiParams);

  const fetchData = (async () => {
    const url: string = `https://api.coronavirus.data.gov.uk/v1/data?${encodedParams}`;
    console.log(url);
    const response = await fetch(url);
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