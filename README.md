# Random issue referencing axios.post

This repo hopefully demonstrates an issue we're seeing, where `npm run dev` S3 uploads using vapor-js all good, but randomly fails after `npm run build` is run. 

#### Config chosen from `laravel new`:
- Laravel Jetstream starter pack
- Vue with Inertia
- API support selected
- PHPUnit test system

S3 bucket has the requisite CORS for local dev

### `npm run dev`
- Everything uploads to S3 all good

### `npm run build`
- We get `Bc.default.post is not a function` from the `await axios.post` request in `Vapor.store()`
- Something about axios maybe?

If we run the following, then the upload _sometimes_ works, but I'm unable to identify exactly why or how:
```bash
 rm -rf node_modules && rm package-lock.json && rm -rf public/build && npm install && npm run build --force && art view:clear
```

.. then if we run `npm run build` again, we get `Bc.default.post is not a function` again. Hmmmmm!
