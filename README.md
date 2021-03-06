# kmeans-Interactive-App-by-shiny

#Shiny Interactive  kmeans  app 

#DEMO webpage

watch the demo from the http://shiny.rstudio.com/gallery/kmeans-example.html

copy right for shiny.rstudio.com 

#What is Shiny 
Shiny is an R package that makes it easy to build interactive web apps straight from R

This example will help  you to buit kmeans Shiny apps

# installed the Shiny package first
open an R session, connect to the internet, and run

install.packages("shiny")

#first file have to be created and saved server.R 
# you need add the function for input, output, and the  session
 
function(input, output, session) {
 
  # Combine the selected variables into a new data frame
  selectedData <- reactive({
    iris[, c(input$xcol, input$ycol)]
  })
  
  clusters <- reactive({
    kmeans(selectedData(), input$clusters)
  })
  
  output$plot1 <- renderPlot({
    palette(c("#E41A1C", "#377EB8", "#4DAF4A", "#984EA3",
              "#FF7F00", "#FFFF33", "#A65628", "#F781BF", "#999999"))
    
    par(mar = c(5.1, 4.1, 0, 1))
    plot(selectedData(),
         col = clusters()$cluster,
         pch = 20, cex = 3)
    points(clusters()$centers, pch = 4, cex = 4, lwd = 4)
  })
  
}

# you need UI app so create file and save it as ui.R  

pageWithSidebar(
  headerPanel('Iris k-means clustering'),
  sidebarPanel(
    selectInput('xcol', 'X Variable', names(iris)),
    selectInput('ycol', 'Y Variable', names(iris),
                selected=names(iris)[[2]]),
    numericInput('clusters', 'Cluster count', 3,
                 min = 1, max = 12)
  ),
  mainPanel(
    plotOutput('plot1')
  )
)

#run both 

# enjoy
