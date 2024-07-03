// Replace with your own API key
const apiKey = 'YOUR_API_KEY'; // Replace with your Google API key
const searchEngineId = 'YOUR_SEARCH_ENGINE_ID'; // Replace with your Google Custom Search Engine ID

const searchForm = document.getElementById('searchForm');
const searchInput = document.getElementById('searchInput');
const searchResults = document.getElementById('searchResults');

searchForm.addEventListener('submit', function(event) {
  event.preventDefault();
  const searchTerm = searchInput.value.trim();
  if (searchTerm === '') return;

  const url = `https://www.googleapis.com/customsearch/v1?key=${apiKey}&cx=${searchEngineId}&q=${searchTerm}`;

  fetch(url)
    .then(response => response.json())
    .then(data => {
      displayResults(data.items);
    })
    .catch(error => {
      console.error('Error fetching search results:', error);
    });
});

function displayResults(items) {
  searchResults.innerHTML = '';

  items.forEach(item => {
    const resultItem = document.createElement('div');
    resultItem.classList.add('result-item');

    const title = document.createElement('h3');
    title.textContent = item.title;
    const link = document.createElement('a');
    link.href = item.link;
    link.target = '_blank'; // Open link in new tab
    link.textContent = item.link;

    const snippet = document.createElement('p');
    snippet.textContent = item.snippet;

    resultItem.appendChild(title);
    resultItem.appendChild(link);
    resultItem.appendChild(snippet);

    searchResults.appendChild(resultItem);
  });
}

