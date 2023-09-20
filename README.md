package com.hcsc.claims.uis.util;

import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.GregorianCalendar;

import javax.xml.datatype.DatatypeConfigurationException;
import javax.xml.datatype.DatatypeConstants;
import javax.xml.datatype.DatatypeFactory;
import javax.xml.datatype.XMLGregorianCalendar;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Formatter {
  
  private final static Logger LOGGER = LoggerFactory.getLogger(Formatter.class);

  private Formatter(){
    
  }
  
  public static XMLGregorianCalendar dateToXMLGregorianCal(Date date) {
    GregorianCalendar c = new GregorianCalendar();
    c.setTime(date);
    XMLGregorianCalendar xmlDate = null;
    try {
      xmlDate = DatatypeFactory.newInstance().newXMLGregorianCalendar(c);
    } catch (DatatypeConfigurationException e) {
      LOGGER.error(e.toString());
    }
    return xmlDate;
  }

  public static Date xmlGregorianCalToDate(XMLGregorianCalendar date) {
    if (date == null) {
      return null;
    } else {
      return date.toGregorianCalendar().getTime();
    }
  }

  /**
   * Convert java.util.Date to XMLGregorianCalendar without TimeZone information
   * @param date
   * @return XMLGregorianCalendar w/o timezone information
   */
  public static XMLGregorianCalendar dateToXMLGregorianDate(Date date) {
    XMLGregorianCalendar xmlDate = dateToXMLGregorianCal(date);
    xmlDate.setTimezone(DatatypeConstants.FIELD_UNDEFINED);
    return xmlDate;
  }

  public static XMLGregorianCalendar parseDate(String date) throws ParseException {
    final DateFormat formatter = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ssX");
    return dateToXMLGregorianDate(formatter.parse(date));
  }

  public static String formatDate(XMLGregorianCalendar date) {
    if (date == null) {
      return "<not set>";
    }
    final DateFormat formatter = new SimpleDateFormat("MM/dd/yyyy");
    return formatter.format(xmlGregorianCalToDate(date));
  }

}
