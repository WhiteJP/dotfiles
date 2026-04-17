# ~/.Rprofile — personal R defaults (symlinked from dotfiles)
# Keep lean: project .Rprofile files (e.g. renv) take precedence when present.

options(
  renv.config.pak.enabled = TRUE
)

if (interactive()) {
  options(
    warn = 1,
    usethis.full_name = "Joshua P. White"
  )

  suppressMessages(require(devtools, quietly = TRUE))
  suppressMessages(require(usethis, quietly = TRUE))

  if (requireNamespace("pak", quietly = TRUE) && getRversion() >= "4.0.0") {
    globalCallingHandlers(
      packageNotFoundError = function(err) {
        try(pak::handle_package_not_found(err))
      }
    )
  }
}
