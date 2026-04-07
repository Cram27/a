/**
 * dynamic-workshops.js
 * Manages the automatic loading and rendering of workshops from CSV files.
 */

async function loadWorkshops() {
    const workshopsContainer = document.getElementById('workshops-grid');
    if (!workshopsContainer) return;

    let csvFiles = [
        'tallers/cca_export__ceramica_2026-04-02.csv'
    ];

    try {
        // Attempt auto-discovery if the server allows directory listing
        const dirResponse = await fetch('tallers/');
        if (dirResponse.ok) {
            const html = await dirResponse.text();
            const parser = new DOMParser();
            const doc = parser.parseFromString(html, 'text/html');
            const links = Array.from(doc.querySelectorAll('a'));
            const discoveredFiles = links
                .map(a => a.getAttribute('href'))
                .filter(href => href && href.endsWith('.csv'))
                .map(href => href.startsWith('tallers/') ? href : `tallers/${href}`);
            
            if (discoveredFiles.length > 0) {
                // Use Set to avoid duplicates and filter out nulls/random strings
                csvFiles = [...new Set([...csvFiles, ...discoveredFiles])].filter(f => f.includes('.csv'));
            }
        }
    } catch (e) {
        console.log('Auto-discovery not supported by server, using defaults.');
    }

    try {
        let allWorkshops = [];

        for (const file of csvFiles) {
            const response = await fetch(file);
            if (!response.ok) continue;
            
            const csvText = await response.text();
            const data = parseCSV(csvText);
            allWorkshops = [...allWorkshops, ...data];
        }

        renderWorkshops(allWorkshops);
    } catch (error) {
        console.error('Error loading workshops:', error);
    }
}

/**
 * Parses a CSV string into an array of objects.
 * Expects the format: ID,"Título (Original)","Título (Traducción)","URL del Post (Original)","URL del Post (Traducción)","URL Imagen Destacada"
 */
function parseCSV(text) {
    const lines = text.split(/\r?\n/).filter(line => line.trim() !== '');
    if (lines.length < 2) return [];

    const headers = parseCSVLine(lines[0]);
    const results = [];

    for (let i = 1; i < lines.length; i++) {
        const values = parseCSVLine(lines[i]);
        if (values.length < headers.length) continue;

        const entry = {};
        headers.forEach((header, index) => {
            // Clean header name
            const cleanHeader = header.replace(/^"|"$/g, '').trim();
            entry[cleanHeader] = values[index] ? values[index].replace(/^"|"$/g, '').trim() : '';
        });
        results.push(entry);
    }

    return results;
}

/**
 * Handles CSV line splitting with support for quotes.
 */
function parseCSVLine(line) {
    const result = [];
    let cur = '';
    let inQuotes = false;
    for (let i = 0; i < line.length; i++) {
        const char = line[i];
        if (char === '"') {
            inQuotes = !inQuotes;
        } else if (char === ',' && !inQuotes) {
            result.push(cur);
            cur = '';
        } else {
            cur += char;
        }
    }
    result.push(cur);
    return result;
}

/**
 * Renders the workshop cards into the DOM.
 */
function renderWorkshops(workshops) {
    const container = document.getElementById('workshops-grid');
    if (!container) return;

    // Get current language from document
    const currentLang = document.documentElement.lang || 'ca';

    container.innerHTML = workshops.map((workshop, index) => {
        const title = currentLang === 'ca' ? workshop['Título (Original)'] : workshop['Título (Traducción)'];
        const url = currentLang === 'ca' ? workshop['URL del Post (Original)'] : workshop['URL del Post (Traducción)'];
        const image = workshop['URL Imagen Destacada'];
        const type = workshop['Tipus de tallers'] || 'Taller';

        // Fix HTML entities like &#8217;
        const cleanTitle = title.replace(/&#8217;/g, "'");

        return `
            <div class="group h-full flex flex-col bg-card-light dark:bg-card-dark rounded-3xl overflow-hidden shadow-md hover:shadow-xl transition-all duration-300 border border-gray-100 dark:border-gray-800 animate-fade-in" style="animation-delay: ${index * 0.1}s">
                <div class="relative overflow-hidden aspect-video">
                    <img src="${image}" alt="${cleanTitle}" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" onerror="this.src='https://via.placeholder.com/400x225?text=Ceramica'">
                    <div class="absolute top-4 left-4 bg-primary text-white text-xs font-bold px-3 py-1 rounded-full uppercase tracking-widest shadow-md">${type}</div>
                </div>
                <div class="p-5 flex flex-col flex-grow space-y-3">
                    <h3 class="font-serif font-bold text-lg md:text-xl text-secondary dark:text-blue-300 leading-tight">${cleanTitle}</h3>
                    <div class="flex-grow"></div>
                    <a href="${url}" target="_blank" class="inline-flex items-center justify-center w-full bg-white dark:bg-transparent text-primary dark:text-white border-2 border-primary hover:bg-primary hover:text-white text-sm font-bold py-3 rounded-xl transition-all duration-300 group/btn">
                        <span data-i18n="cta_book">${currentLang === 'ca' ? 'Reserva el taller' : 'Reserva el taller'}</span>
                        <span class="material-symbols-outlined ml-2 text-sm group-hover/btn:translate-x-1 transition-transform">arrow_forward</span>
                    </a>
                </div>
            </div>
        `;
    }).join('');
}

// Initial load
document.addEventListener('DOMContentLoaded', loadWorkshops);

// Listen for language changes if the function exists
const originalChangeLanguage = window.changeLanguage;
window.changeLanguage = function(lang) {
    if (typeof originalChangeLanguage === 'function') {
        originalChangeLanguage(lang);
    }
    // Re-render workshops with the new language
    loadWorkshops();
};
