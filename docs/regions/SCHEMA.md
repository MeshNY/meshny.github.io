# Region map data schema

This folder contains a portable static region-map viewer. An organization may
copy `map.html`, publish an `index.json` beside it, and host each referenced
GeoJSON file locally or on a separate HTTPS origin.

`index.json` is the public authority for the map title and each region's
identity and coordination status. GeoJSON supplies geometry and optional
descriptive/provenance data; its coordination fields are ignored by the viewer.

## `index.json`

The manifest must be a JSON object containing a `regions` array. Each region
item represents one map layer and must include `id` and `file`. Use a `name`
and `short_name` for every item; these are used for stable layer names, colors,
the legend, and popup content.

```json
{
  "title": "Example Mesh Region Map",
  "regions": [
    {
      "id": "example",
      "name": "Example Mesh Region",
      "short_name": "EXAMPLE",
      "region_type": "Regional",
      "coordination_status": "coordinated_external",
      "coordination_label": "Coordinated External Region",
      "file": "example.geojson"
    }
  ]
}
```

### Top-level fields

| Field | Required | Description |
| --- | --- | --- |
| `title` | Recommended | Map title shown in the browser tab and map key. |
| `regions` | Yes | Array of region-layer objects. |

### Region fields

| Field | Required | Description |
| --- | --- | --- |
| `id` | Yes | Stable, unique region identifier. It overrides every GeoJSON feature's `id`. |
| `name` | Recommended | Human-readable region name. |
| `short_name` | Recommended | Short region code shown on the map. |
| `region_type` | No | Boundary category shown in popups. |
| `coordination_status` | Recommended | Public status controlling the badge and boundary style. If omitted, the viewer uses `extrapolated_external`. |
| `coordination_label` | No | Optional text for the status badge. The viewer supplies a standard label when omitted. |
| `file` | Yes | Local GeoJSON filename/path or an absolute `https://` GeoJSON URL. |

Use one of these stable values for `coordination_status`:

| Value | Meaning in this viewer |
| --- | --- |
| `official_new_england` | Official New England Mesh Region |
| `official_local` | Official region of the organization hosting the map |
| `political_boundaries` | Political Boundaries |
| `proposed` | Proposed Region |
| `coordinated_external` | Coordinated External Region |
| `extrapolated_external` | Suggested External Region |

Local `file` paths resolve relative to the region-map directory. Absolute URLs
allow a coordinator to operate their own GeoJSON endpoint:

```json
{
  "id": "ny",
  "name": "New York",
  "short_name": "NY",
  "coordination_status": "coordinated_external",
  "file": "https://nyme.sh/regions/nyc.geojson"
}
```

`index.json` is strict JSON, so do not add comments to it. The viewer also
accepts a legacy array-only manifest, but new maps should use the object form.

## GeoJSON files

Each `file` must return a GeoJSON `FeatureCollection` with a `features` array.
One or more polygon or multipolygon features are typical:

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "boundary_basis": "Coordinator-defined operating area",
        "notes": "Reviewed July 2026",
        "source": "Example Mesh regional coordinators"
      },
      "geometry": {
        "type": "Polygon",
        "coordinates": [[[-73.9, 42.7], [-73.2, 42.7], [-73.2, 43.1], [-73.9, 43.1], [-73.9, 42.7]]]
      }
    }
  ]
}
```

Feature properties such as `kind`, `boundary_basis`, `notes`, `draft`, and
`source` may be included. When both the manifest and a feature contain the same
ordinary property, the manifest value wins.

Do not use `coordination_status`, `coordination_label`, or
`coordination_notes` in GeoJSON to declare public status. The viewer discards
those fields and derives status only from `index.json`.

## Hosting on another website

An external host must serve the GeoJSON over HTTPS and allow the map site's
origin with CORS, for example:

```text
Access-Control-Allow-Origin: https://newenglandme.sh
```

`Access-Control-Allow-Origin: *` also works for public GeoJSON. The endpoint
must return a successful HTTP response and `application/geo+json` or
`application/json` is recommended. If CORS is missing or the endpoint is down,
the browser will block the request and the map will show a loading error.
