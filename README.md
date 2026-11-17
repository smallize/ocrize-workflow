# OCRize production workflows

The six manually dispatched workflows deploy about.ocrize.com, products.ocrize.com, and www.ocrize.com/app/ai/cloud exclusively to production Ceph. They use Hugo 0.125.7 extended and the `production_ceph` targets from smallize/ocrize. Staging choices have been removed.

Repository secrets: REPO_TOKEN for source checkout; CEPH_ACCESS_KEY_ID and CEPH_SECRET_ACCESS_KEY for the restricted OCRize production deployer. AWS deployment credentials are not used. CloudFront invalidation is disabled; DNS/CDN routing is unchanged.

Each workflow serializes deployments for its domain, validates build output, and checks the published pages, referenced assets, gzip responses, content types, and HTTP 404 handling. products.ocrize.cloud is excluded.

Menu validation runs before and after deployment. Every rendered menu must load `https://menucdn.containerize.com/core/engine.min.js?v=1.0.1`. The CDN engine, menu JSON, and menu images (including CSS background logos) must return HTTP 200 with nonempty bodies and valid image content types.
