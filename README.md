# REST Countries: Where in the World? ([View Live](https://rest-countries.app))

![Homepage screenshot](./public/screenshot.png)

## Table of Contents

- [Overview](#overview)
  - [What is REST Countries?](#what-is-rest-countries)
  - [Features](#features)
  - [Technology Stack](#technology-stack)
- [Development Process](#development-process)
  - [Purpose and Goals](#purpose-and-goals)
  - [Encountered Challenges](#encountered-challenges)
  - [What I Learned](#what-i-learned)
- [Author](#author)
- [License](#license)

## Overview

### What is REST Countries?

REST Countries is a **comprehensive country database/explorer designed to help people get up-to-date country information through an interactive card-based interface**. The web application provides detailed country data, including population, regional information, languages, currencies, and neighboring countries, while making the search process much easier and faster by offering a search by name and filter by region functionality.

This is a single-page web application built with TypeScript and React displaying the country data fetched from the REST Countries API using React Router data loaders. The web application incorporates modern and responsive UI with startup/upbeat design personality adapted to mobile, tablet and desktop screens built using SCSS Modules for granular component-first styling.

### Features

- **🌗 Color Theme Switcher** - A light/dark color theme switcher built with React Context API and Sass improving accessibility and user experience by storing user’s choice across browser sessions using LocalStorage Web API.
- **⚡ Modern React Router** - Data fetching with React Router data loaders reducing page load times by leveraging render-as-you-fetch approach.
- **📦 Code Splitting** - Code splitting reducing page load times and bundle size by streaming in the needed data using React.lazy() and Suspense API.

### Technology Stack

![Static Badge](https://img.shields.io/badge/React-gray?style=for-the-badge&color=%23ced4da)
![Static Badge](https://img.shields.io/badge/React_Router-gray?style=for-the-badge&color=%23ced4da)
![Static Badge](https://img.shields.io/badge/TypeScript-gray?style=for-the-badge&color=%23ced4da)
![Static Badge](https://img.shields.io/badge/Sass-gray?style=for-the-badge&color=%23ced4da)
![Static Badge](https://img.shields.io/badge/REST_Countries_API-gray?style=for-the-badge&color=%23ced4da)

## Development Process

### Purpose and Goals

My motivation for building this project stemmed from wanting to iterate on my web development skills and consolidate my React knowledge through leveraging advanced React patterns and real-world API integration. I aimed to create a more complex web application that incorporates popular features like color theme switching, client-side filtering, pagination and data streaming.

My goal was to learn how to **use external RESTFul and Web APIs**.

### Encountered Challenges

When I started implementing infinite scroll for the country card list on the homepage, I realized that, unfortunately, the **REST Countries API does not provide a built-in pagination endpoint**, so I had to handle it myself on the client side. I limited the number of displayed cards to 10 units per page and then expanded the array of displayed countries each time the user moves to the next page by tracking the last displayed card using the useCallback React Hook and the Intersection Observer Web API.

**Here is a snippet that shows how I implemented client-side pagination to create the infinite scroll effect**:

```typescript
const COUNTRIES_PER_PAGE = 10;

const shownCountries = filteredCountries.slice(0, page * COUNTRIES_PER_PAGE);

const observerRef = useRef<IntersectionObserver>();
const lastCountryCardRef = useCallback(
  (node: HTMLLIElement | null) => {
    observerRef.current?.disconnect();

    if (!node) return;

    observerRef.current = new IntersectionObserver((entries) => {
      if (entries[0]?.isIntersecting) {
        onMoveToNextPage();
      }
    });

    observerRef.current.observe(node);
  },
  [onMoveToNextPage],
);
```

The second challenge I faced was to **make the page bookmarkable** to ensure users would never lose their search context and could instantly share what they're viewing with others. To implement this functionality, I stored the search input and the region filter values as search parameters by leveraging React Router's built-in useSearchParams hook.

**Here is a snippet that shows how I stored the UI state of the search input and the region filter in the URL**:

```typescript
const [searchParams, setSearchParams] = useSearchParams();

const [searchedCountryName, setSearchedCountryName] = useState(
  searchParams.get("countryName") ?? "",
);
const [searchedCountryRegion, setSearchedCountryRegion] = useState(
  searchParams.get("countryRegion") ?? "",
);

function handleChangeSearchedCountryName(searchedCountryName: string) {
  setPage(1);
  setSearchedCountryName(searchedCountryName);
  searchParams.set("countryName", searchedCountryName);
  setSearchParams(searchParams);
}

function handleChangeSearchedCountryRegion(searchedCountryRegion: string) {
  setPage(1);
  setSearchedCountryRegion(searchedCountryRegion);
  searchParams.set("countryRegion", searchedCountryRegion);
  setSearchParams(searchParams);
}
```

### What I Learned

I learned a lot about **how to integrate and work with external RESTful APIs** and **how to leverage Web APIs like LocalStorage and Intersection Observer** to implement advanced UI features.

## Author

Built by **Danil Dikhtyar** - Front-end developer creating modern websites / web applications.

**Connect with me:**

- 🌐 Portfolio: [dikhtyar.dev](https://dikhtyar.dev)
- 📫 Email: [contact@dikhtyar.dev](mailto:contact@dikhtyar.dev)
- 🐦 Twitter: [@Rock_n_Roll_CRC](https://x.com/Rock_n_Roll_CRC)

_Feel free to reach out for collaborations or questions about this project!_

## License

Copyright (c) 2025 Danil Dikhtyar. All rights reserved.

Licensed under the MIT License as stated in the [LICENSE](LICENSE):

```text
Copyright (c) 2025 Danil Dikhtyar

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
