<!DOCTYPE html>
<html>
<head>
  <title>Google Sheets Mirror</title>
</head>
<body>
  <table id="data-table">
    <thead>
      <tr>
        <th>Name</th>
        <th>Email</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>

  <script>
    // Load the Google Sheets API asynchronously
    function loadSheetsAPI() {
      const script = document.createElement('script');
      script.src = 'https://apis.google.com/js/api.js';
      script.onload = handleAPILoaded;
      document.body.appendChild(script);
    }

    // API loaded callback
    function handleAPILoaded() {
      gapi.load('client', initClient);
    }

    // Initialize the API client
    function initClient() {
      gapi.client.init({
        apiKey: '<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSuxhf9YQEuj6Z4qnLvXr9KFMr-nXosjbqcevKESA2KkwP5F8qKT9tnslOTzHdZW4tz7smEz-OGZlWv/pubhtml?widget=true&amp;headers=false"></iframe>',
        discoveryDocs: ['https://sheets.googleapis.com/$discovery/rest?version=v4'],
      }).then(() => {
        // Call the function to fetch data
        getDataFromGoogleSheet();
      });
    }

    // Fetch data from Google Sheet
    function getDataFromGoogleSheet() {
      gapi.client.sheets.spreadsheets.values.get({
        spreadsheetId: 'YOUR_SPREADSHEET_ID',
        range: 'Sheet1!A2:B', // Adjust the range as per your data
      }).then((response) => {
        const data = response.result.values;

        // Populate the table with data
        const tableBody = document.querySelector('#data-table tbody');
        data.forEach((row) => {
          const newRow = document.createElement('tr');
          row.forEach((cell) => {
            const newCell = document.createElement('td');
            newCell.textContent = cell;
            newRow.appendChild(newCell);
          });
          tableBody.appendChild(newRow);
        });
      }, (error) => {
        console.error('Error fetching data from Google Sheet:', error);
      });
    }

    // Load the Sheets API
    loadSheetsAPI();
  </script>
</body>
</html>

