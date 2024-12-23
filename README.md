// Какой USERAGENT в программе axios
// Mozilla/5.0 (X11; Linux x86_64; rv:134.0) Gecko/20100101 Firefox/134.0
const axios = require('axios');
const fs = require('fs');

function saveWebsiteToFile(url, outputFile) {
  axios
    .get(url, {
      headers: {
        'User-Agent':
          'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36', // Set your custom user agent
      },
    })
    .then((response) => {
      fs.writeFile(outputFile, response.data, (err) => {
        if (err) {
          console.error('Error writing to file', err);
        } else {
          console.log(`Website saved to ${outputFile}`);
        }
      });
    })
    .catch((error) => {
      if (error.response && error.response.status === 404) {
        console.log('phone not found');
      } else {
        console.error('Error fetching the website', error);
      }
    });
}

// Example usage:
const url = 'https://whatmyuseragent.com/'; // Replace with the URL you want to save
const outputFile = 'website.html'; // Output file name
saveWebsiteToFile(url, outputFile);
