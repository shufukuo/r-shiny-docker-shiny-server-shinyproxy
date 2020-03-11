#
FROM rocker/shiny:3.6.1

#
#ENV DEBIAN_FRONTEND=noninteractive

# install R packages
RUN R -e "install.packages( c('shinyjs', 'shinyBS', 'DT', 'ggplot2', 'magrittr', 'data.table', 'reticulate', 'rmarkdown'), repos='https://cran.rstudio.com/')"

# install chinese fonts for R ggplot
RUN apt update && apt install -y \
	xfonts-base fonts-wqy-zenhei fonts-arphic-bkai00mp fonts-arphic-bsmi00lp fonts-arphic-gbsn00lp fonts-arphic-gkai00mp fonts-arphic-ukai fonts-arphic-uming fonts-cns11643-kai fonts-cns11643-sung fonts-cwtex-fs fonts-cwtex-heib fonts-cwtex-kai fonts-cwtex-ming fonts-cwtex-yen

# install python3 packages
RUN apt update && apt install -y \
	python3-venv python3-pip

RUN pip3 install pandas==0.25.1 && \
	pip3 install numpy==1.17.4 && \
	pip3 install odps && \
	pip3 install elasticsearch==6.4.0

# copy configuration files into the Docker image
COPY shiny-server.conf /etc/shiny-server/shiny-server.conf
COPY shiny-server.sh /usr/bin/shiny-server.sh

# create folder of shiny app files
RUN mkdir /srv/shiny-server/myapp

#RUN chmod -R 755 /srv/shiny-server/

# set port
EXPOSE 3838

CMD ["/usr/bin/shiny-server.sh"]
