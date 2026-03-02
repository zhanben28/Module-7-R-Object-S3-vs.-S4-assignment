# Module-7-R-Object-S3-vs.-S4-assignment
data("airquality")
head(airquality, 6)
list(airquality)

summary(airquality)
print(airquality)
mean(airquality$Temp)
typeof(airquality)
class(airquality)
is.list(airquality)

#S3 Example
air_reading_s3 <- list(
  date    = "May 1",
  ozone   = 41,
  wind    = 7.4,
  temp    = 67
)

class(air_reading_s3) <- "AirReading"

is.list(air_reading_s3)
attr(air_reading_s3, "class")

print.AirReading <- function(x) {
  cat("Air Quality Reading\n")
  cat("Date:        ", x$date, "\n")
  cat("Ozone (ppb): ", x$ozone, "\n")
  cat("Wind (mph):  ", x$wind, "\n")
  cat("Temp (F):    ", x$temp, "\n")
}

print(air_reading_s3)

isS4(air_reading_s3)
typeof(air_reading_s3)

#S4 Example
setClass("AirReadingS4", representation(
  date  = "character",
  ozone = "numeric",
  wind  = "numeric",
  temp  = "numeric"
))

setGeneric("describe", function(object) standardGeneric("describe"))

setMethod("describe", "AirReadingS4", function(object) {
  cat("Air Quality Reading\n")
  cat("Date:        ", object@date, "\n")
  cat("Ozone (ppb): ", object@ozone, "\n")
  cat("Wind (mph):  ", object@wind, "\n")
  cat("Temp (F):    ", object@temp, "\n")
})

air_reading_s4 <- new("AirReadingS4",
  date  = "May 1",
  ozone = 41,
  wind  = 7.4,
  temp  = 67
)

air_reading_s4

describe(air_reading_s4)

air_reading_s4@temp
air_reading_s4@ozone

isS4(air_reading_s4)
typeof(air_reading_s4)
