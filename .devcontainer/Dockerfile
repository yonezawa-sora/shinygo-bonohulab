FROM rocker/r-ver:latest

# Install system dependencies
RUN apt-get update && apt-get install -y \
    libcurl4-gnutls-dev \
    libssl-dev \
    libxml2-dev \
    libgit2-dev \
    libsqlite3-dev \
    libcairo2-dev \
    libxt-dev

# Install R packages
RUN R -e "install.packages(c('shiny', 'RSQLite', 'ggplot2', 'gridExtra', 'plotly', 'reshape2', 'visNetwork', 'DT', 'STRINGdb', 'pathview', 'dplyr', 'shinyBS', 'shinyjs', 'reactable'), dependencies = TRUE)"

# defalt command R
CMD ["R"]

# Expose port 3838
EXPOSE 3838