# Reuters GraphQL Schema

Conceptual GraphQL schema for the Reuters Connect API. Reuters Connect Web Services provides a professional REST API for searching and retrieving editorial content — text, images, video, and graphics — from Reuters and partner content sources. This GraphQL schema represents the same content model in a typed, query-driven form.

## Source

- Developer portal: https://developer.reuters.com/
- Reuters Connect developer docs: https://developers.reutersconnect.com/docs
- Authentication: https://developers.reutersconnect.com/authentication

## Schema File

[reuters-schema.graphql](reuters-schema.graphql)

## Type Summary

| Type | Description |
|------|-------------|
| `Article` | A single editorial article distributed via Reuters Connect |
| `ArticleDetails` | Extended metadata — word count, urgency, GUID, embargo status |
| `ArticleType` | Enum: TEXT, ADVISORY, CORRECTION, RECAP, FEATURE, ANALYSIS, BREAKING, BACKGROUND |
| `ArticleStatus` | Enum: USABLE, WITHHELD, CANCELLED, REPLACED, EMBARGOED |
| `Headline` | Text, priority, long/short/sub head, catchline, language |
| `HeadlinePriority` | Enum: FLASH, URGENT, REGULAR, ADVANCE, ROUTINE |
| `Story` | A grouping of related articles with slug, package, and topics |
| `StoryDetails` | Summary, byline, dateline, credit line, editor note |
| `StoryPackage` | Curated themed story bundles with lead story |
| `StorySlug` | URL-safe story identifier with canonical form |
| `Body` | Full article body: rawHtml, rawText, paragraphs, structured content |
| `BodyContent` | A structured content unit (type, value, attributes) |
| `BodyParagraph` | An indexed paragraph with text and role |
| `Media` | Generic media asset: photo, video, graphic, audio |
| `MediaDetails` | Filename, MIME type, dimensions, duration, color space |
| `MediaType` | Enum: PHOTO, VIDEO, GRAPHIC, AUDIO, DOCUMENT, PACKAGE |
| `MediaVersion` | A specific rendition of a media asset with URL and dimensions |
| `Photo` | A photographic asset with EXIF, caption, and licensing |
| `PhotoDetails` | Camera make/model, exposure, focal length, ISO, orientation |
| `PhotoCaption` | Text, long/short caption, credit line, byline, dateline |
| `Video` | A video asset with clips, caption, and topics |
| `VideoDetails` | Duration, frame rate, aspect ratio, resolution, codec, bitrate |
| `VideoCaption` | Text, long/short caption, credit line, byline, language |
| `VideoClip` | A timecoded clip segment within a video asset |
| `Gallery` | An editorial photo gallery with ordered photos |
| `GalleryPhoto` | A photo in a gallery with position and featured flag |
| `Topic` | A Reuters taxonomy topic tag with parent/child hierarchy |
| `TopicDetails` | Display name, description, language, aliases |
| `TopicCode` | A topic code with scheme identifier |
| `Subject` | An IPTC or Reuters subject classification |
| `SubjectCode` | A subject code with scheme identifier |
| `Geography` | A geographic region or location with hierarchy |
| `GeographyDetails` | Name, ISO codes, latitude/longitude, aliases |
| `GeoCode` | A geographic code with scheme identifier |
| `GeoType` | Enum: WORLD, CONTINENT, REGION, COUNTRY, STATE, CITY, DISTRICT, VENUE |
| `Person` | A person referenced in editorial content |
| `PersonDetails` | First/last name, title, role, nationality, description, aliases |
| `Organization` | An organization referenced in editorial content |
| `OrganizationDetails` | Name, ticker, exchange, ISIN, sector, country, website |
| `Author` | A Reuters or contributing author with bio and articles |
| `AuthorDetails` | Display name, email, Twitter, location |
| `AuthorBio` | Short/long bio, photo URL, specializations |
| `Source` | A content source or partner provider |
| `SourceDetails` | Name, code, description, website, country, trust status |
| `Wire` | A Reuters wire or content channel |
| `WireService` | Wire metadata: name, code, content types, languages, channels |
| `WireItem` | A single item delivered on a wire with channel and sequence |
| `DateRange` | An inclusive date range (from/to) |
| `SearchQuery` | Structured search input with keywords, taxonomy filters, date range |
| `SearchFilter` | Output representation of applied search filters |
| `SearchResults` | Combined search results with article list, media, and facets |
| `SearchFacets` | Aggregated facet buckets for topics, subjects, geographies, etc. |
| `FacetBucket` | A label/value/count tuple for a facet dimension |
| `ArticleResults` | Paginated list of articles with total count |
| `PageInfo` | Pagination metadata: page, perPage, totalPages, cursors |
| `LanguageCode` | Enum: EN, DE, FR, ES, AR, ZH, JA, PT, RU, IT |
| `ContentPriority` | Enum: FLASH, URGENT, HIGH, NORMAL, LOW, ADVANCE |
| `ContentType` | Enum: TEXT, PHOTO, VIDEO, GRAPHIC, AUDIO, PACKAGE, DATA |
| `License` | License terms for Reuters content (reuse, modification, attribution) |
| `Distribution` | Distribution scope, regions, platforms, embargo |
| `APIToken` | A time-limited bearer token returned after authentication |
| `APIKey` | An API key credential with scopes and active status |

## Key Queries

```graphql
# Retrieve a single article by ID
query GetArticle($id: ID!) {
  article(id: $id) {
    id
    headline { text priority }
    body { rawText paragraphs { index text } }
    topics { details { name } }
    author { details { displayName } }
    publishedAt
  }
}

# Search articles with filters
query SearchArticles($q: SearchQuery) {
  search(query: $q) {
    totalCount
    articles {
      items {
        id
        headline { text }
        contentType
        priority
        publishedAt
      }
      page { page perPage totalPages hasNextPage }
    }
  }
}

# Fetch a photo with all renditions
query GetPhoto($id: ID!) {
  photo(id: $id) {
    id
    details { width height cameraModel }
    caption { text creditLine byline }
    versions { label url width height }
    license { name requiresAttribution }
  }
}

# Fetch wire items for a date range
query GetWireItems($wireId: ID!, $range: DateRange) {
  wireItems(wireId: $wireId, dateRange: $range, limit: 50) {
    id
    priority
    channel
    transmittedAt
    article { id headline { text } }
  }
}

# Obtain an API token
mutation Authenticate($keyId: ID!, $secret: String!) {
  createAPIToken(keyId: $keyId, secret: $secret) {
    token
    expiresAt
    tokenType
    scope
  }
}
```

## Content Channels

Reuters Connect organizes content into channels by category:

| Channel Code | Description |
|---|---|
| `TXT` | Text articles and advisories |
| `PIX` | Photography |
| `VID` | Video |
| `GFX` | Graphics and infographics |

## Notes

- Authentication uses OAuth 2.0 client credentials. Call `createAPIToken` with your API key ID and secret to receive a bearer token valid for the session.
- Content priority drives delivery order on the wire: FLASH > URGENT > HIGH > NORMAL.
- Embargo dates are respected; `ArticleStatus.EMBARGOED` items carry an `embargoDate` in `ArticleDetails`.
- The taxonomy (topics, subjects, geographies) follows a mix of Reuters internal codes and IPTC NewsCodes.
- `SearchFacets` allow drilling into results without re-querying from scratch.
